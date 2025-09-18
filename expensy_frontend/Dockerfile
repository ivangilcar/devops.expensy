# Etapa 1: Build
FROM node:20-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
# Generamos la build standalone
RUN npm run build

# Etapa 2: Runtime
FROM node:20-alpine
WORKDIR /app

# Copiamos solo lo necesario del builder
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public

# Si necesitas variables de entorno en runtime
ENV NODE_ENV=production

EXPOSE 3000
CMD ["node", "server.js"]
