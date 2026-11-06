FROM node:22-bookworm-slim
WORKDIR /app
COPY package.json server.mjs ./
COPY public ./public
RUN mkdir -p /data && chown node:node /data
USER node
ENV NODE_ENV=production PORT=3000 DB_PATH=/data/store.sqlite
EXPOSE 3000
CMD ["node","server.mjs"]
