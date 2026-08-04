# IntelliView Orchestrator

The **IntelliView Orchestrator** is an AI-powered distributed interview orchestration framework. It manages real-time, multi-modal AI interviews using a robust architecture designed for high availability, fault tolerance, and comprehensive analytics.

## Project Architecture

- **FastAPI**: The core backend API framework handling routing, validation, and orchestration logic.
- **Next.js 14**: A real-time frontend dashboard for HR personnel to monitor and review interviews.
- **PostgreSQL**: Primary persistent data store for session data, configurations, and analytical reporting.
- **Redis**: In-memory caching and message broker for the task queue.
- **Celery**: Asynchronous worker pool handling heavy AI processing tasks (audio transcription, evaluation, hallucination detection).
- **CV Service**: Dedicated computer vision microservice.
- **Monitoring**: Built-in integration with Prometheus, Grafana, and Jaeger for tracing and metric tracking.

## Getting Started

### Prerequisites

Ensure you have Docker and Docker Compose installed on your system.
For local native development, you will need Python 3.10+ and Node.js 20+.

### Running with Docker Compose (Recommended)

The easiest way to spin up the entire application stack is via Docker Compose. This brings up the API, Frontend, PostgreSQL, Redis, Celery Workers, Flower (task monitoring), and observability tools.

```bash
# Build and start the complete environment in detached mode
docker-compose up -d --build
```

### Useful Endpoints

Once the stack is running, you can access the following services locally:

- **Frontend HR Dashboard**: [http://localhost:3000](http://localhost:3000)
- **FastAPI Backend Swagger Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Flower (Celery Monitor)**: [http://localhost:5555](http://localhost:5555)
- **Grafana (Dashboards)**: [http://localhost:3001](http://localhost:3001)
- **Jaeger (Tracing)**: [http://localhost:16686](http://localhost:16686)
- **Prometheus (Metrics)**: [http://localhost:9090](http://localhost:9090)

## Development Setup

### Backend

1. Navigate to the root directory.
2. Install Python dependencies: `pip install -r requirements.txt`
3. Start the FastAPI server natively: `uvicorn orchestrator.main:app --host 0.0.0.0 --port 8000`

### Frontend

1. Navigate to the frontend directory: `cd frontend`
2. Install Node dependencies: `npm ci`
3. Run the development server: `npm run dev`

## Running Tests

We use `pytest` for backend testing and `vitest` for the frontend.

```bash
# Run backend tests
pytest tests/ -v -m "not e2e"

# Run frontend tests
cd frontend
npm run test
```

## Troubleshooting & Maintenance

If you encounter issues with database schema drift, ensure Alembic migrations are up to date.
To bring down the entire stack and wipe volumes (destructive action):
```bash
docker-compose down -v
```
