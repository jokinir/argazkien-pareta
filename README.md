# argazkien-pareta

A minimal proof of concept for the Argazkien Pareta backend and containerized development setup.

## Repository layout

- `src/backend/` — Django backend project and container build files
- `src/frontend/` — frontend placeholder for future UI work

## Local development

Start the backend and PostgreSQL database with Docker Compose:

```bash
docker compose up --build
```

Then open `http://localhost:8000/` to verify the backend service.

## Notes

- Backend framework: Django
- Database: PostgreSQL
- Current focus: backend API containerized with Docker Compose

