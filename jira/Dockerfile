# FROM node:16
# WORKDIR /app
# COPY ./app.js ./package.json ./
# RUN npm install
# EXPOSE 3000
# CMD [ "node", "app.js" ]



FROM node:16 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .


FROM node:16-alpine
WORKDIR /app
COPY --from=builder /app/package*.json /app/app.js ./
COPY --from=builder /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "app.js"]