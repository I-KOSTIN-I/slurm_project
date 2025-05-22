# Сборка
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# Релиз
FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json .

EXPOSE 3000

HEALTHCHECK --interval=10s --timeout=2s --start-period=5s CMD wget -q --spider http://localhost:3000 || exit 1

CMD ["npm", "start"]
