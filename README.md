[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/psqlpy?style=for-the-badge)](https://pypi.org/project/psqlpy/)
[![PyPI](https://img.shields.io/pypi/v/psqlpy?style=for-the-badge)](https://pypi.org/project/psqlpy/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/psqlpy?style=for-the-badge)](https://pypistats.org/packages/psqlpy)

# PSQLPy - Async PostgreSQL driver for Python written in Rust.

Driver for PostgreSQL written fully in Rust and exposed to Python.
Main goals of the library is speed and type safety.

## Documentation
You can find full documentation here - [PSQLPy documentation](https://psqlpy-python.github.io/)

## Installation

You can install package with `pip` or `poetry`.

poetry:

```bash
> poetry add psqlpy
```

pip:

```bash
> pip install psqlpy
```

Or you can build it by yourself. To do it, install stable rust and [maturin](https://github.com/PyO3/maturin).

```
> maturin develop --release
```

## Usage

Usage is as easy as possible.
Create new instance of ConnectionPool and start querying.
You don't need to startup connection pool, the connection pool will create connections as needed.

```python
from typing import Any

from psqlpy import ConnectionPool, QueryResult


async def main() -> None:
    db_pool = ConnectionPool(
        username="postgres",
        password="pg_password",
        host="localhost",
        port=5432,
        db_name="postgres",
        max_db_pool_size=2,
    )

    res: QueryResult = await db_pool.execute(
        "SELECT * FROM users",
    )

    print(res.result())
    db_pool.close()

```

## Benchmarks

You can find benchmarks with visualization on our [docs](https://psqlpy-python.github.io/benchmarks.html)
