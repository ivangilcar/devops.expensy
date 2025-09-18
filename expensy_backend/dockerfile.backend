# Etapa 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

# Copiamos dependencias
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y build
COPY . .
RUN npm run build

# Etapa 2: Runtime
FROM node:20-alpine

WORKDIR /app

# Copiamos solo lo necesario
COPY --from=builder /app/package*.json ./
RUN npm install --omit=dev

COPY --from=builder /app/dist ./dist

ENV NODE_ENV=production

EXPOSE 8706
CMD ["node", "dist/server.js"]
