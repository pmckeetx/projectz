FROM node:lts as build

ARG NODE_ENV=production
ENV NODE_ENV $NODE_ENV

ARG REACT_APP_SERVICE_HOST=http://localhost:8080
ENV REACT_APP_SERVICE_HOST $REACT_APP_SERVICE_HOST

WORKDIR /code

COPY package.json /code/package.json
COPY package-lock.json /code/package-lock.json
RUN npm ci

COPY . /code
RUN npm run build



FROM nginx:1.12-alpine

COPY --from=build /code/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

# ARG PORT=80
# ENV PORT $PORT