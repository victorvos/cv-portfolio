---
description: Code Style and DRY Principles
---

# Python Development Guidelines

Standards for writing clean, maintainable, and SOLID Python code.

## Code Organization

### File Size Limits
- **Routers/Controllers**: < 400 lines
- **Services**: < 300 lines
- **Utilities**: < 200 lines
- **Interfaces**: < 100 lines
- **Functions**: < 50 lines (extract if longer)
- **Classes**: < 300 lines (single responsibility)

### Module Structure
```
project/
├── core/              # Domain logic (no framework dependencies)
│   ├── config/        # Settings and configuration
│   ├── entities/      # Domain models (dataclasses/Pydantic)
│   ├── interfaces/    # Abstract base classes
│   └── services/      # Business logic services
├── infrastructure/    # External implementations
│   ├── external/      # Third-party API integrations
│   ├── repositories/  # Database access
│   └── schemas/       # Serialization models
├── presentation/      # API/UI layer
│   └── api/
│       ├── dependencies.py   # DI hooks
│       ├── models.py         # Request/response models
│       └── *_router.py       # Route handlers
└── utils/             # Pure utility functions
```

## SOLID Principles

### Single Responsibility (SRP)
Each module has one reason to change:
```python
# Good: Focused service
class EmailService:
    def send_email(self, to: str, subject: str, body: str): ...

# Bad: Multiple responsibilities
class UserService:
    def create_user(self): ...
    def send_welcome_email(self): ...  # Should be EmailService
    def generate_report(self): ...     # Should be ReportService
```

### Open/Closed (OCP)
Open for extension, closed for modification:
```python
# Good: Strategy pattern
class PaymentProcessor:
    def __init__(self, strategy: IPaymentStrategy):
        self.strategy = strategy

    def process(self, amount: float):
        return self.strategy.execute(amount)

# Bad: Switch statements that grow
def process_payment(method: str, amount: float):
    if method == "stripe": ...
    elif method == "paypal": ...  # Adding new methods requires modification
```

### Liskov Substitution (LSP)
Subtypes must be substitutable for base types:
```python
# Good: Subclass honors contract
class Bird(ABC):
    @abstractmethod
    def move(self): ...

class Sparrow(Bird):
    def move(self): return self.fly()

class Penguin(Bird):
    def move(self): return self.swim()  # Still moves, different implementation
```

### Interface Segregation (ISP)
Prefer small, focused interfaces:
```python
# Good: Focused interfaces
class IReadable(ABC):
    @abstractmethod
    def read(self) -> bytes: ...

class IWritable(ABC):
    @abstractmethod
    def write(self, data: bytes): ...

# Bad: Fat interface
class IFile(ABC):
    @abstractmethod
    def read(self): ...
    @abstractmethod
    def write(self): ...
    @abstractmethod
    def compress(self): ...  # Not all files need this
```

### Dependency Inversion (DIP)
Depend on abstractions, not concretions:
```python
# Good: Inject interface
class OrderService:
    def __init__(self, repo: IOrderRepository, notifier: INotifier):
        self.repo = repo
        self.notifier = notifier

# Bad: Concrete dependency
class OrderService:
    def __init__(self):
        self.repo = PostgresOrderRepository()  # Tightly coupled
```

## Coding Standards

### Type Hints
Always use type hints for function signatures:
```python
def process_data(items: list[dict[str, Any]], limit: int = 10) -> list[str]:
    ...

async def fetch_user(user_id: str) -> Optional[User]:
    ...
```

### Docstrings
Use Google-style docstrings for public APIs:
```python
def calculate_total(items: list[Item], discount: float = 0.0) -> float:
    """Calculate the total price of items with optional discount.

    Args:
        items: List of items to calculate
        discount: Discount percentage (0.0 to 1.0)

    Returns:
        Total price after discount

    Raises:
        ValueError: If discount is outside valid range
    """
```

### Naming Conventions
```python
# Classes: PascalCase
class UserService: ...
class IOrderRepository: ...  # Interface prefix

# Functions/methods: snake_case
def get_user_by_id(): ...
async def process_payment(): ...

# Constants: UPPER_SNAKE_CASE
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 30

# Private: _leading_underscore
def _helper_function(): ...
_internal_cache = {}
```

### Error Handling
```python
# Good: Specific exceptions
class EntityNotFoundError(Exception):
    """Raised when entity doesn't exist."""

class ValidationError(Exception):
    """Raised for invalid input."""

# Usage
try:
    user = await repo.get_user(user_id)
except EntityNotFoundError:
    raise HTTPException(status_code=404, detail="User not found")
```

### Async/Await
```python
# Good: Concurrent execution when possible
async def fetch_all_data():
    users, orders = await asyncio.gather(
        fetch_users(),
        fetch_orders()
    )
    return users, orders

# Avoid: Sequential when parallelism is possible
async def fetch_all_data():
    users = await fetch_users()  # Waits
    orders = await fetch_orders()  # Then waits again
```

## Dependency Injection

### FastAPI Pattern
```python
# dependencies.py
def get_db() -> Database:
    return container.database()

def get_user_service(db: Database = Depends(get_db)) -> UserService:
    return UserService(db)

# router.py
@router.get("/users/{id}")
async def get_user(
    user_id: str,
    service: UserService = Depends(get_user_service)
) -> User:
    return await service.get_by_id(user_id)
```

### Service Injection
```python
class Container:
    """Dependency injection container."""

    @cached_property
    def config(self) -> Settings:
        return Settings()

    @cached_property
    def database(self) -> Database:
        return Database(self.config.DATABASE_URL)

    @cached_property
    def user_service(self) -> UserService:
        return UserService(self.database)
```

## Testing Guidelines

### Structure
```python
# tests/unit/test_user_service.py
class TestUserService:
    def test_create_user_with_valid_data(self):
        # Arrange
        service = UserService(mock_repo)

        # Act
        result = service.create(valid_user_data)

        # Assert
        assert result.id is not None

    def test_create_user_with_invalid_email_raises_error(self):
        service = UserService(mock_repo)

        with pytest.raises(ValidationError):
            service.create({"email": "invalid"})
```

### Mocking
```python
@pytest.fixture
def mock_repository():
    repo = Mock(spec=IUserRepository)
    repo.get_by_id.return_value = User(id="1", name="Test")
    return repo

def test_with_mock(mock_repository):
    service = UserService(mock_repository)
    result = service.get_user("1")
    assert result.name == "Test"
```

## When to Extract

Extract code to a new module when:
1. A function exceeds 50 lines
2. A class has unrelated methods (violates SRP)
3. Code is duplicated across files
4. A file exceeds size limits
5. Testing requires mocking internals
6. Circular imports occur
