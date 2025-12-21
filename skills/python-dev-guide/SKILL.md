---
name: python-dev-guide
description: This guide describes the rules you need to follow when developing Python code. Recommended to use when writing, reading, and analyzing python code
---

# Python Development Guide

This skill provides Python development principles and best practices. Follow these guidelines when writing, reviewing, or analyzing Python code.

## Code Style (PEP 8)

### Naming Conventions

```python
# modules/packages: lowercase, underscores
import my_module

# classes: PascalCase
class UserAccount:
    pass

# functions/variables: snake_case
def calculate_total():
    user_count = 0

# constants: UPPER_SNAKE_CASE
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 30

# private: single underscore prefix
def _internal_helper():
    pass

# "mangled" (avoid name collision): double underscore prefix
class Base:
    def __private_method(self):
        pass
```

### Formatting

- **Line length**: Max 88 characters (Black default), but string type exception
- **Indentation**: 4 spaces (never tabs)
- **Blank lines**: 2 between top-level definitions, 1 between methods
- **Imports**: Standard library, third-party, local (each group separated by blank line)

```python
import os
import sys

import requests
from fastapi import FastAPI

from myproject.utils import helper
```

## Type Annotations (Required)

```python
from typing import Optional, List, Dict, Callable, TypeVar, Generic

T = TypeVar('T')

def process_items(
    items: List[str],
    callback: Optional[Callable[[str], None]] = None
) -> Dict[str, int]:
    """Process items and return counts."""
    ...

# Use | for unions (Python 3.10+)
def fetch_user(user_id: int) -> User | None:
    ...
```

## Docstrings (Google Style)

```python
def calculate_total(prices: List[float], tax_rate: float = 0.1) -> float:
    """Calculate total price including tax.

    Args:
        prices: List of item prices.
        tax_rate: Tax rate as decimal. Defaults to 0.1.

    Returns:
        Total price with tax applied.

    Raises:
        ValueError: If prices contains negative values.

    Example:
        >>> calculate_total([10.0, 20.0], 0.1)
        33.0
    """
    ...
```

## Error Handling

```python
# Use specific exceptions with context
raise ValueError(f"Invalid user_id: {user_id}. Must be positive integer.")

# Never use bare except
try:
    result = risky_operation()
except SpecificError as e:
    logger.error(f"Operation failed: {e}")
    raise

# Use context managers for resources
from contextlib import contextmanager

@contextmanager
def managed_resource():
    resource = acquire_resource()
    try:
        yield resource
    finally:
        release_resource(resource)

# Custom exceptions for domain errors
class DomainError(Exception):
    """Base exception for domain errors."""
    pass

class ValidationError(DomainError):
    """Raised when validation fails."""
    pass
```

## Architecture Principles

- **Composition over inheritance**: Reduce coupling through composition
- **Dependency injection**: Improve testability and flexibility
- **SOLID principles**: Single responsibility, Open-closed, Liskov substitution, Interface segregation, Dependency inversion
- **Explicit over implicit**: Prefer clear, readable code over clever tricks

```python
# Dependency injection example
class UserService:
    def __init__(self, repository: UserRepository, cache: Cache):
        self._repository = repository
        self._cache = cache

    def get_user(self, user_id: int) -> User:
        if cached := self._cache.get(user_id):
            return cached
        user = self._repository.find(user_id)
        self._cache.set(user_id, user)
        return user
```

## Testing (pytest)

```python
import pytest
from unittest.mock import Mock, patch

class TestUserService:
    @pytest.fixture
    def mock_repository(self):
        return Mock(spec=UserRepository)

    @pytest.fixture
    def service(self, mock_repository):
        return UserService(repository=mock_repository)

    def test_get_user_returns_user(self, service, mock_repository):
        # Arrange
        expected_user = User(id=1, name="Test")
        mock_repository.find.return_value = expected_user

        # Act
        result = service.get_user(1)

        # Assert
        assert result == expected_user
        mock_repository.find.assert_called_once_with(1)

    @pytest.mark.parametrize("user_id,expected", [
        (1, "admin"),
        (2, "user"),
    ])
    def test_get_user_role(self, service, user_id, expected):
        ...
```

## Performance

- **Async/await** for I/O-bound operations
- **Generators** for memory-efficient iteration
- **Appropriate data structures**: `set` for membership, `dict` for lookup, `deque` for queues
- **Caching** with `functools.lru_cache` or `functools.cache`

```python
import asyncio
from functools import lru_cache

# Async I/O
async def fetch_all(urls: List[str]) -> List[Response]:
    async with aiohttp.ClientSession() as session:
        tasks = [fetch_one(session, url) for url in urls]
        return await asyncio.gather(*tasks)

# Caching expensive computations
@lru_cache(maxsize=128)
def expensive_calculation(n: int) -> int:
    ...

# Generator for large datasets
def process_large_file(path: str):
    with open(path) as f:
        for line in f:
            yield transform(line)
```

## Development Workflow

1. **Analyze codebase** - Review existing patterns before implementing
2. **Small increments** - Write small segments, test immediately
3. **Fix errors first** - Never proceed with broken code
4. **Write tests** - Test each module upon completion
5. **Document public APIs** - Docstrings for all public functions/classes
