# Docker Compose Scripts for NestJS Application

## Development Server

Run the development server with hot reload:

```bash
# Using the development-specific compose file
docker-compose -f docker-compose.dev.yml up --build

# Or using the main compose file with development environment
docker-compose --env-file .env.dev up --build
```

## Production Server

Run the production server:

```bash
# Using the production-specific compose file
docker-compose -f docker-compose.prod.yml up --build

# Or using the main compose file with production environment
docker-compose --env-file .env.prod up --build
```

## Available Commands

### Development

```bash
# Start development server
npm run docker:dev

# Start development server in detached mode
npm run docker:dev:detached

# Stop development server
npm run docker:dev:stop
```

### Production

```bash
# Start production server
npm run docker:prod

# Start production server in detached mode
npm run docker:prod:detached

# Stop production server
npm run docker:prod:stop
```

### General

```bash
# Clean up containers, networks, and volumes
npm run docker:clean

# View logs
docker-compose logs -f nestjs
```

## Environment Variables

### Development (.env.dev)

- `TARGET=development` - Docker build target
- `NODE_ENV=development` - Node environment
- `PORT=3000` - Application port
- Volume mounting enabled for hot reload

### Production (.env.prod)

- `TARGET=production` - Docker build target
- `NODE_ENV=production` - Node environment
- `PORT=3000` - Application port
- No volume mounting for security

## Features

- **Multi-stage builds**: Optimized images for development and production
- **Hot reload**: Development mode includes volume mounting for live code changes
- **Environment separation**: Different configurations for dev/prod
- **Security**: Production runs as non-root user
- **Networking**: Isolated Docker network for services
- **Easy cleanup**: Scripts to stop and clean up containers
