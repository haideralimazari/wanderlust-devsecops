# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Use the production env if available, otherwise fallback to sample
RUN if [ -f .env.docker ]; then cp .env.docker .env.local; else cp .env.sample .env.local; fi

RUN npm run build

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:21-slim

WORKDIR /app

COPY --from=frontend-builder /app .

EXPOSE 5173

CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "5173"]

