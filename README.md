# Traefik Auth Request Demo

A demonstration of request authentication using Traefik's ForwardAuth middleware with a Flask-based auth service.

## Overview

This project shows how to implement authentication at the gateway level using:
- **Traefik** as the reverse proxy with ForwardAuth middleware
- **Flask** service for authentication validation
- **File provider** with YAML configuration (matching Kubernetes cluster setup)

## Testing

See [TESTING.md](TESTING.md) for testing steps and test cases.

## Project Structure

```
.
├── auth/             # Flask auth service
│   ├── auth.py       # Authentication logic
│   └── Dockerfile    # Auth service container
├── traefik/          # Traefik configuration
│   ├── traefik.yml   # Main Traefik config
│   └── dynamic/      # Dynamic configuration
│       ├── auth-middleware.yml
│       └── ingressroute.yml
├── docker-compose.yml
└── README.md
```
