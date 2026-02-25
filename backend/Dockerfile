# Stage 1: builder - install all deps
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

# Stage 2: production - only prod deps + app code
FROM node:18-alpine AS production
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --from=builder /app/server.js ./
EXPOSE 8080
CMD ["node", "server.js"]
