# Stage 1: build/install
FROM node:20-bookworm-slim AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev

# Stage 2: runtime — distroless, không có shell, không package manager
FROM gcr.io/distroless/nodejs20-debian12
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY server.js ./
ENV PORT=3000
EXPOSE 3000
USER nonroot
CMD ["server.js"]