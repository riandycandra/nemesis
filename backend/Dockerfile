FROM node:20-slim

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci --omit=dev

COPY src ./src
COPY seed ./seed
COPY scripts ./scripts

RUN mkdir -p /app/data /app/dataset && chown -R node:node /app

USER node

EXPOSE 3000

CMD ["node", "src/server.js"]
