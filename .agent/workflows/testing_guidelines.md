---
description: Unified Testing Strategy
---

# Testing Guidelines

Standards for ensuring code reliability through automated tests.

## Testing Layers

### 1. Unit Tests (`tests/unit/`)
**Scope**: Isolated functions/classes.
**Dependencies**: Mock EVERYTHING.
**Speed**: Instant (< 10ms per test).

```python
def test_calculate_discount():
    # Arrange
    item = Item(price=100)

    # Act
    result = calculate_discount(item, 0.1)

    # Assert
    assert result == 90
```

### 2. Integration Tests (`tests/integration/`)
**Scope**: Interaction between 2+ modules (e.g., Service + DB).
**Dependencies**: Use real DB (via container/test DB) but mock 3rd party APIs.
**Speed**: Moderate (< 5s per test).

```python
@pytest.mark.asyncio
async def test_user_creation_with_db(db_session):
    repo = UserRepository(db_session)
    user = await repo.create(email="test@darom.com")
    assert user.id is not None
```

### 3. End-to-End (E2E) Tests (`tests/e2e/`)
**Scope**: Full system flow.
**Dependencies**: Full deployment (Docker/Staging).
**Speed**: Slow (Minutes).

## Tools & Libraries

### Pytest
We use standard `pytest` conventions.

- **Files**: `test_*.py`
- **Functions**: `test_*`
- **Fixtures**: Defined in `conftest.py`

### Mocking
Use `unittest.mock` or `pytest-mock`.

```python
def test_service_calls_repo(mocker):
    mock_repo = mocker.Mock()
    service = UserService(mock_repo)

    service.do_work()

    mock_repo.save.assert_called_once()
```

## Coverage Rules

- **Core Logic**: 100% coverage required.
- **Utils**: 80% coverage required.
- **Infrastructure**: Smoke tests only (don't test 3rd party libraries).

## Running Tests

```bash
# Run all
pytest tests/

# Run specific layer
pytest tests/unit/

# Watch mode (dev)
ptw tests/
```
