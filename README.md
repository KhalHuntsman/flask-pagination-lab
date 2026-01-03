# Flask Pagination Lab

### Overview

This project is a **Flask-based REST API** that demonstrates **server-side pagination** using SQLAlchemy.  
The API exposes a `/books` endpoint that supports query-based pagination and returns structured metadata alongside paginated results.

The goal of this lab is to replace an inefficient “return everything” API pattern with a scalable, production-ready pagination approach commonly used in real-world APIs such as GitHub, Reddit, and Shopify.

This project emphasizes:
- Efficient database querying
- Clean API response design
- Test-driven development with Pytest
- Backend-first responsibility for data slicing and metadata

### Features

- Paginated `/books` API endpoint
- Query parameters for `page` and `per_page`
- Safe handling of out-of-range page requests
- Deterministic ordering for predictable pagination
- Structured JSON responses with pagination metadata
- Fully tested using Pytest

### Pagination Behavior

The `/books` endpoint supports the following query parameters:

- `page` — the page number to retrieve (default: `1`)
- `per_page` — number of records per page (default: `5`)

### Example Request
GET /books?page=2&per_page=3

clean

### Example Response
```json
{
  "page": 2,
  "per_page": 3,
  "total": 20,
  "total_pages": 7,
  "items": [
    { "id": 4, "title": "Book 4", "author": "Flatiron School" },
    { "id": 5, "title": "Book 5", "author": "Flatiron School" },
    { "id": 6, "title": "Book 6", "author": "Flatiron School" }
  ]
}
If a page exceeds the available range, the API returns an empty list while preserving metadata.

### Technologies & Tools Used
#### Backend
- Python 3

#### Flask
- Flask-RESTful
- Flask-SQLAlchemy
- Marshmallow

#### Database
- SQLite (development & testing)

#### Testing
- Pytest

#### Tooling
- Pipenv
- Git & GitHub

### File Structure
All paths are listed relative to the project root.

- flask-pagination-lab/.pytest_cache/
- flask-pagination-lab/server/instance/
- flask-pagination-lab/server/migrations/
- flask-pagination-lab/server/testing/conftest.py
- flask-pagination-lab/server/testing/pagination_test.py
- flask-pagination-lab/server/app.py
- flask-pagination-lab/server/config.py
- flask-pagination-lab/server/models.py
- flask-pagination-lab/server/seed.py
- flask-pagination-lab/.gitignore
- flask-pagination-lab/Pipfile
- flask-pagination-lab/Pipfile.lock
- flask-pagination-lab/pytest.ini
- flask-pagination-lab/README.md

### Key Files Explained
#### server/app.py
- Main Flask application entry point.
- Defines the /books API endpoint and implements pagination logic using SQLAlchemy’s .paginate() method.

#### server/models.py
- Defines the Book SQLAlchemy model and corresponding Marshmallow schema used for serialization.

#### server/config.py
- Application factory and database configuration.
- Initializes Flask, SQLAlchemy, and Flask-RESTful.

#### server/seed.py
- Populates the database with sample book data for local development and testing.

#### server/testing/pagination_test.py
- Pytest test suite validating pagination behavior, defaults, edge cases, and response structure.

### Testing Notes
- Tests use an in-memory database
- Database schema is created and destroyed per test session
- No migrations are run during testing
- Pagination logic is validated entirely through API requests

- Run tests with: pytest
#### Running the Project
##### Setup

- pipenv install && pipenv shell
- cd server

- flask db init
- flask db migrate -m "initial migration"
- flask db upgrade head
- python seed.py

- Run the Server: python app.py
- Visit: http://localhost:5555/books

## License
Educational use only.
Intended for learning Flask API design, pagination strategies, and backend testing.