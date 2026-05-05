FROM node:18-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci --only=production

FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/node_modules/ ./node_modules/
COPY server.js .
COPY views/ views/

EXPOSE 4000

CMD ["node", "server.js"]