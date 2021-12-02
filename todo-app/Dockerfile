FROM node:16.8.0 AS builder

ARG URL

WORKDIR /usr/src/app/

COPY package*.json ./

RUN npm install

COPY ./ ./

RUN REACT_APP_API_URL=${URL} npm run build

FROM nginx:alpine

WORKDIR /usr/share/nginx/html/

RUN rm -rf ./*

COPY --from=builder /usr/src/app/build ./

ENTRYPOINT ["nginx", "-g", "daemon off;"]