# Use Node.js 18 Alpine as base image
FROM node:22-alpine AS base
WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm ci --only=production && npm cache clean --force

# Development stage
FROM node:22-alpine AS development
WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm ci
COPY . .
EXPOSE 3000
CMD ["npm", "run", "start:dev"]

# Build stage
FROM node:22-alpine AS build
WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm ci
COPY . .
RUN npm run build

# Production stage
FROM node:22-alpine AS production
WORKDIR /app

# Copy production dependencies from base stage
COPY --from=base /app/node_modules ./node_modules
COPY --from=build /app/dist ./dist
COPY package.json ./

# Expose port
EXPOSE 3000

# Start the application
CMD ["npm", "run", "start:prod"]