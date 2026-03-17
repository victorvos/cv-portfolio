---
description: FastAPI Routing and API Guidelines
---

# FastAPI Best Practices

Guidelines for structuring FastAPI routes and request handling.

## Router Organization

Split routers by domain logic, not technical function.

```
presentation/api/
├── routes/
│   ├── auth.py         # /auth endpoints
│   ├── properties.py   # /properties endpoints
│   └── users.py        # /users endpoints
├── __init__.py         # Export routers
└── deps.py            # Global dependencies
```

## Darom API Path Structure

**The API router is mounted at `/api` (NOT `/api/v1`).**

| Component | Prefix | Final Path Example |
|:---|:---|:---|
| Main app | `/api` | - |
| ai_services router | `/ai` | `/api/ai/generate-article` |
| articles router | - | `/api/articles/{id}` |
| comments router | - | `/api/comments/{id}` |
| voting router | - | `/api/votes/{id}` |
| websocket router | `/ws` | `/api/ws/article/{id}` |

When calling API endpoints from JavaScript:
```javascript
// Correct
fetch('/api/ai/editor/chat', { ... })

// Incorrect - do NOT use /api/v1
fetch('/api/v1/ai/editor/chat', { ... })  // 404!
```

## Request lifecycle

### 1. Pydantic Models (DTOs)
Use separate models for Request (Input) and Response (Output).

```python
# Create Request
class UserCreate(BaseModel):
    email: EmailStr
    password: SecretStr

# Read Response
class UserRead(BaseModel):
    id: UUID
    email: EmailStr
    is_active: bool

    class Config:
        from_attributes = True
```

### 2. Dependency Injection
Use `Depends` for services, current user, and common logic.

```python
@router.post("/items/", response_model=ItemRead)
async def create_item(
    item: ItemCreate,
    current_user: User = Depends(get_current_active_user),
    service: ItemService = Depends(get_item_service)
):
    return await service.create(user=current_user, data=item)
```

## Best Practices

### Status Codes
- `200 OK`: Standard success (GET, PATCH).
- `201 Created`: Creation success (POST).
- `204 No Content`: Deletion success response (DELETE).
- `400 Bad Request`: Validation errors.
- `401 Unauthorized`: Authentication missing/invalid.
- `403 Forbidden`: Authentication valid but permission denied.
- `404 Not Found`: Resource doesn't exist.

### Error Handling
Raise `HTTPException` in the router or service layer.

```python
from fastapi import HTTPException

if not item:
    raise HTTPException(
        status_code=404,
        detail=f"Item with id {id} not found"
    )
```

### Query Parameters
Group search/filter params into a dependency class if there are many.

```python
@dataclass
class CommonQueryParams:
    q: str | None = None
    skip: int = 0
    limit: int = 100

@router.get("/items/")
async def read_items(commons: CommonQueryParams = Depends()):
    return commons
```
