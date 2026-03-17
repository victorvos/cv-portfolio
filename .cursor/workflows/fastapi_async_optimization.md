---
description: Guide for optimizing FastAPI server responsiveness, handling blocking I/O, and ensuring optimal UX via global notifications.
---

# FastAPI Async Concurrency & Service Optimization

This workflow outlines the strategy for building high-performance, responsive AI web applications using FastAPI. It addresses the common "stuck server" issue caused by blocking synchronous calls and ensures a smooth user experience even during heavy background processing.

## 1. Audit External Services (The "Blocking" Check)
Most Python SDKs for AI (e.g., specific older versions of OpenAI, Google GenAI, xAI) effectively make **blocking synchronous HTTP requests**, even if called within an `async` route. This freezes the entire FastAPI event loop (or at least the single worker).

**Checklist:**
- [ ] Identify all external API calls.
- [ ] Check if the SDK method is definitively `async await` (e.g., uses `httpx.AsyncClient`).
- [ ] If it is `def` (sync) or standard `requests`, it **must** be offloaded.

## 2. Offload Blocking Calls to ThreadPool
Do **not** call synchronous blocking functions directly in an `async def` endpoint. Wrap them in `run_in_executor`.

### Pattern
```python
import asyncio

# Bad (Blocks the loop)
# result = sync_client.chat.create(...)

# Good (Non-blocking)
async def run_sync_ai_call(prompt: str):
    loop = asyncio.get_running_loop()
    # Execute in default ThreadPoolExecutor
    return await loop.run_in_executor(
        None,
        lambda: sync_client.chat.create(prompt=prompt)
    )
```

## 3. Background Tasks & Worker Concurrency
For operations taking > 2 seconds (like Verification or Deep Research), do not make the user wait for the HTTP response.

### Backend Strategy
1.  **Accept Request**: Validate input and credits immediately.
2.  **Queue Task**: Use `FastAPI.BackgroundTasks` or a dedicated queue (Celery/Redis) for multi-server setups. For single-server, `BackgroundTasks` + Memory Set is sufficient.
3.  **Return Immediately**: Return a `202 Accepted` or `200 OK` with status "processing".

### Server Configuration
Default `uvicorn` runs 1 worker. If that worker is busy (even with async, CPU-bound tasks can block), the site stalls.
**Production Rule**: Always run multiple workers.
```yaml
# docker-compose.yml
command: uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

## 4. Global UX & Real-Time Notifications
Users will navigate away while long tasks run. You must reach them wherever they are.

### Global Notification Architecture
1.  **User Stream**: On the frontend, maintain a **persistent** WebSocket connection subscribed to `user_{user_id}`. This is distinct from the page-specific 'article' channel.
2.  **Backend Broadcast**: When the background task finishes, emit the event to the **User Room**.
    ```python
    await websocket_service.broadcast_to_room(
        room=f"user_{user_id}",
        message={"type": "task_complete", "title": "...", "status": "success"}
    )
    ```
3.  **Frontend Handling**:
    - **If on target page**: Update the specific UI component (e.g., turn "Verify" badge green).
    - **If elsewhere**: Show a global "Toast" notification (e.g., "✅ Verification Complete: [Title]").

## Summary Checklist for New Features
- [ ] **IO Analysis**: Is the core logic async? If not, wrap it.
- [ ] **Concurrency**: Is the server running with >1 worker?
- [ ] **Feedback**: Does the user get immediate feedback (optimistic UI)?
- [ ] **Persistence**: Can the user leave the page and still get the result? (Global Websocket).
