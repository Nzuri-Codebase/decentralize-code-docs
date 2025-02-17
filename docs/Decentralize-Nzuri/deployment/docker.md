# Docker Deployment

## Overview
* The Decentralize Nzuri web application is containerized using Docker, allowing for easy deployment and scalability. 
* The application includes three main services:
    1. **Streamlit**: The frontend web interface for Honda and Nissan applications.
    2. **Flask API**: Handles user authentication and session tracking.
    3. **InfluxDB**: Stores time-series data for user login/logout events.

## Dockerfiles
Each service has its own Dockerfile for building the container image

## Docker Compose
The `docker-compose.yml` file orchestrates the deployment of all three services:
```yaml
version: '3.8'
services:
  streamlit:
    build:
      dockerfile: ./Dockerfile
      context: ./streamlit
    ports:
      - "8081:8501"
  flask:
    build:
      dockerfile: ./Dockerfile
      context: ./flask
    ports:
      - "5000:5000"
  influxdb:
    build:
      dockerfile: ./Dockerfile
      context: ./influxdb
    ports:
      - "8086:8086"
```

## Running the Application
1. Build the Docker images:
```bash
docker-compose build
```
2. Start the containers:
```bash
docker-compose up
```
3. Access the application at `http://localhost:8081`

## Error Handling
- The application includes basic error handling for:
    - Docker build errors
    - Container startup failures
    - SSL certificate generation errors

## Output
- The application runs in Docker containers, accessible via HTTP/HTTPS.

## Limitations
- Requires proper configuration.