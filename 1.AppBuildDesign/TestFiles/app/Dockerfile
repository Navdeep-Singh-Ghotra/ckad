FROM node:current-alpine3.20
# FROM node:20-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
