FROM node:12-alpine3.15

WORKDIR /app
RUN mkdir src e2e

# ---- Dependencies ----
COPY ./package*.json ./
RUN npm install

# ---- Build ----
COPY karma.conf.js ./
COPY *.json ./
COPY ./e2e /app/e2e
COPY ./src /app/src
RUN npm run build --prod

EXPOSE 4200

CMD ["npm", "start"]