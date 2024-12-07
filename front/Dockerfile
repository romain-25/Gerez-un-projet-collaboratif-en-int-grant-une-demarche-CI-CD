FROM node:latest as build

WORKDIR /usr/local/app

COPY ./package.json ./yarn.lock /usr/local/app/

RUN yarn install

COPY ./ /usr/local/app/

RUN npm run build

FROM nginx:latest as production

RUN adduser --disabled-login --gecos '' appuser

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

USER appuser

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
