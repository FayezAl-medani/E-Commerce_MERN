FROM node:18-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM node:18-alpine
WORKDIR /app
ENV NODE_ENV=production

COPY package*.json ./
RUN npm ci --production

COPY --from=builder /app/dist ./dist
COPY public ./public

EXPOSE 3001
CMD ["node", "dist/index.js"]
