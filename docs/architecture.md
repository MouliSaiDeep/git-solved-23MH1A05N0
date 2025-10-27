# System Architecture

## Overview
DevOps Simulator follows a microservices architecture designed for high availability and scalability.
This document covers both production and development configurations.
## Components

### 1. Application Server
- **Technology**: Node.js + Express
- **Production Port**: 8080
- **Development Port**: 3000
- **Scaling**: Horizontal auto-scaling enabled
- **Development Features:**: hot reload, Chrome DevTools debugger (port 9229)
- **Notes**: Development uses a single instance with manual scaling.

### 2. Database Layer
- **Database**: PostgreSQL 14
- **Production**: Master-slave replication with daily automated backups
- **Development**: Local single instance, no replication
- **Seeding**: Auto-seed with test data on startup (development only)
- **Backup**: Manual backups in development

### 3. Monitoring System
- **Production**: Prometheus + Grafana with email alerts for critical issues
- **Development**: Basic console logging + Prometheus with console warnings (no email in dev)
- **Metrics**: CPU, Memory, Disk, Network, Build time (development only)
- **Dashboard**: In-development web dashboard

### 4. Container Orchestration (Development Only)
- **Tool**: Docker Compose (local)
- **Services**: App, Database, Redis cache
- **Volume Mounts**: Code directory for hot reload

### 5. Authentication System (Beta - Development)
- **Method**: OAuth2 + JWT
- **Providers**: Google, GitHub (for testing)
- **Sessions**: Redis-based session storage

## Deployment Strategy
### Production
- **Method**: Rolling updates
- **Zero-downtime**: Yes
- **Rollback**: Automated on failure

### Development
- **Method**: Docker Compose hot reload
- **Zero-downtime**: Not applicable (dev environment)
- **Rollback**: Git checkout previous commit
- **Development Workflow**:
    1. Make code changes
    2. Auto-reload triggers rebuild
    3. Run unit tests
    4. Check console logs
    5. Commit when ready

## Security
- **Production**:
    - SSL/TLS encryption
    - Database connection encryption
    - Regular security audits
    
- **Development**:
    - SSL/TLS disabled for local development
    - Database credentials in plain text (dev only)
    - CORS enabled for all origins
    - Debug endpoints exposed

## Experimental Features
⚠️ **Warning**: The following features are experimental:
- Multi-cloud deployment
- AI-powered log analysis
- Automatic rollback on anomaly detection
