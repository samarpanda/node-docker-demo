FROM node:12-stretch AS build-docker
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM nginx:1.17-alpine
COPY --from=build-docker /app/build /usr/share/nginx/html