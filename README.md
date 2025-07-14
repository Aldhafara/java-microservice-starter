# LightPollutionService

![Build](https://github.com/Aldhafara/LightPollutionService/actions/workflows/ci.yml/badge.svg)

![License](https://img.shields.io/github/license/Aldhafara/LightPollutionService)

![Last Commit](https://img.shields.io/github/last-commit/Aldhafara/LightPollutionService)

LightPollutionService provides real-time sky darkness ratings and light pollution data for any location, empowering
astrophotographers to find the best stargazing spots.

## Table of Contents

- [Features](#features)
- [How to Run](#how-to-run)
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
- [Data Source](#data-source)
- [TODO / Roadmap](#todo--roadmap)

## Features

Currently under development. Available now:

- /status health-check endpoint (server status, uptime, timestamp)

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/Aldhafara/LightPollutionService.git
```

2. Start the application:

```bash
./mvnw spring-boot:run
```

3. By default, the application will be available at:

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
| /darkness | GET  | Sky brightness rating for given coordinates | ❌      |

## API Request Parameters

Planned features. Not yet implemented

| Parameter | Type  | Description        | Default            |
|-----------|-------|--------------------|--------------------|
| latitude  | float | Location latitude  | 52.232222 (Warsaw) |
| longitude | float | Location longitude | 21.008333 (Warsaw) |

- **All parameters are optional.** If not provided, Warsaw is used.

**Example requests:**

```
GET /status
GET /darkness
GET /darkness?latitude=50.06143&longitude=19.93658
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

### Example `/darkness` Response

Planned features. Not yet implemented.

```json
{
  "latitude": 52.232222,
  "longitude": 21.008333,
  "radiance": 0.12,
  "darknessScore": "dark"
}
```

**Description of key fields:**

- `latitude`, `longitude` - query coordinates
- `radiance` - light intensity (lower = darker)
- `darknessScore` - sky darkness rating (e.g., "dark", "average", "bright")

## Caching

- Lookup results are cached (planned: per location for 1 hour).
- First request may be slower (file read), subsequent ones are instant.

## Rate Limiting

- Planned: endpoint protection (e.g., /darkness)—limit 20 requests/min/IP.
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
curl "http://localhost:8080/darkness?latitude=50.06143&longitude=19.93658"
```

## How to Test

Run tests:

```bash
./mvnw test
```

## License

MIT

## Data Source

This product was made utilizing VIIRS Nighttime Lights data produced by the Earth Observation Group, Payne Institute for
Public Policy, Colorado School of Mines.

### Data:

[EOG VIIRS Nighttime Lights - annual composites](https://eogdata.mines.edu/products/vnl/#annual_v2)

License: Creative Commons Attribution 4.0 (CC-BY 4.0)

## TODO / Roadmap

- [ ] /darkness?lat=...&lon=... endpoint
- [ ] GeoTIFF value lookup
- [ ] Result caching
- [ ] Input parameter validation
- [X] Global error handler
- [ ] API documentation (Swagger/OpenAPI)
- [ ] Integration tests (MockMvc)
- [ ] Example deployment (Docker/Kubernetes)