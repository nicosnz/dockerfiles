FROM node:22-alpine AS dev
WORKDIR /app
COPY ./app/package*.json ./
RUN npm install

FROM node:22-alpine AS prod
RUN apk add --no-cache curl
WORKDIR /app
COPY --from=dev /app/node_modules ./node_modules
COPY ./app ./
EXPOSE 8082
HEALTHCHECK --interval=10s --timeout=5s --start-period=5s --retries=3 CMD curl -f http://localhost:8082/health
CMD ["node","index.js"]