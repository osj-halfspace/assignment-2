# Anonymous Feedback Platform

A simple internal platform for employees to share anonymous feedback and ideas.

## Project Overview

- **Backend:** Python with **FastAPI**. Uses `uv` for package management and development.
- **Frontend:** **React** with **TypeScript** and **Vite**.
- **Storage:** **In-memory** (no persistent database).
- **Architecture:** RESTful API with CORS enabled for development.

## Building and Running

### Development Mode

The easiest way to start the entire stack is using the provided `start.sh` script:

```bash
./start.sh
```

This script will:
1. Sync backend dependencies using `uv`.
2. Start the FastAPI server on `http://localhost:8000`.
3. Install frontend dependencies using `npm`.
4. Start the Vite development server on `http://localhost:5173`.

### Manual Control

#### Backend
```bash
cd backend
uv sync
uv run fastapi dev main.py --port 8000
```

#### Frontend
```bash
cd frontend
npm install
npm run dev -- --port 5173
```

## Development Conventions

- **API Design:** Follows RESTful principles.
- **Backend Style:** Uses `Annotated` for dependency injection and parameter validation.
- **Frontend Style:** Modern React hooks and TypeScript for type safety.
- **Storage:** Temporary in-memory storage; data is lost on server restart.
