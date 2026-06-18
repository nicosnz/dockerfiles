FROM node:22.11.0-alpine AS dev

WORKDIR /app

COPY package.json ./

RUN npm install

COPY . ./

RUN npm run build

  

FROM nginx:1.27.3-alpine AS prod

COPY --from=dev /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d

CMD [ "nginx","-g","daemon off;"]