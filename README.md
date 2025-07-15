# java-microservice-starter

![Build](https://github.com/Aldhafara/java-microservice-starter/actions/workflows/ci.yml/badge.svg)

![License](https://img.shields.io/github/license/Aldhafara/java-microservice-starter)

![Last Commit](https://img.shields.io/github/last-commit/Aldhafara/java-microservice-starter)

java-microservice-starter is Java/Spring Boot Microservice Skeleton
Reusable starter for building production-ready Java/Spring Boot microservices.

## Table of Contents

- [Features](#features)
- [How to Run](#how-to-run)
- [How to Run with Docker](#how-to-run-with-docker)
- [API Documentation (Swagger/OpenAPI)](#api-documentation-swaggeropenapi)
- [API - Endpoints](#api-endpoints)
- [API - Request Parameters](#api-request-parameters)
- [API Response Format](#api-response-format)
- [Caching](#caching)
- [Rate Limiting](#rate-limiting)
- [Error Handling](#error-handling)
- [Example Usage](#example-usage)
- [How to Test](#how-to-test)
- [License](#license)
- [TODO / Roadmap](#todo--roadmap)

## Features

Currently under development. Available now:

- /status health-check endpoint (server status, uptime, timestamp)

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/Aldhafara/java-microservice-starter.git
```

2. Start the application:

```bash
./mvnw spring-boot:run
```

3. By default, the application will be available at:

```
http://localhost:8080
```

## How to Run with Docker

1. Build the JAR:

```bash
./mvnw clean package
```

2. Build the image:

```bash
docker build -t javamicroservicestarter .
```

3. Run:

```bash
docker run -p 8080:8080 javamicroservicestarter
```

4. (or, with Docker Compose)

```bash
docker compose up --build
```

Once running, the application will be available at:

```
http://localhost:8080
```

## API Documentation (Swagger/OpenAPI)

Once the application is running, interactive API documentation will be available at:

```
http://localhost:8080/swagger-ui.html
```

You can explore, test, and understand all endpoints directly from your browser.
_Planned: As new endpoints are implemented, they will be automatically documented here._

## API Endpoints

| Endpoint  | Type | Description                                 | Status |
|-----------|------|---------------------------------------------|--------|
| /status   | GET  | Server status, uptime, timestamp            | ✅      |

## API Request Parameters

Planned features. Not yet implemented

**Example requests:**

```
GET /status
```

## API Response Format

### Example `/status` Response

```json
{
  "status": "UP",
  "uptime": 5025112,
  "uptimePretty": "1h 23m 45s",
  "timestamp": "2025-07-14T18:52:00Z"
}
```

**Description of key fields:**

- `status` - server status
- `uptime` - server uptime in ms
- `uptimePretty` - server uptime in easy to read form
- `timestamp` - timestamp of request

## Caching

- Lookup results are cached (planned: per location for 1 hour).
- First request may be slower (file read), subsequent ones are instant.

## Rate Limiting

- Planned: endpoint protection (e.g., /template-endpoint)—limit 20 requests/min/IP.
- Exceeding the limit: HTTP 429.

## Error Handling

Planned features. Not yet implemented.

- 503 - if data unavailable (e.g., file read error)
- 422 - invalid input parameters (latitude, longitude)
- All errors in clear JSON format:

```json
{
  "error": "Invalid parameter: latitude",
  "timestamp": "2025-07-14T18:52:00Z"
}
```

## Example Usage

Planned features. Not yet implemented.

```bash
curl "http://localhost:8080/template-endpoint"
```

## How to Test

Run tests:

```bash
./mvnw test
```

## License

MIT

## TODO / Roadmap

- [ ] /template-endpoint
- [ ] Result caching
- [ ] Input parameter validation
- [X] Global error handler
- [ ] API documentation (Swagger/OpenAPI)
- [ ] Integration tests (MockMvc)
- [X] Example deployment (Docker/Kubernetes)