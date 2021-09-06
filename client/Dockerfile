FROM node:alpine as builder
WORKDIR "/app"
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build 

FROM nginx

# node app will run on 3000, so nginx is set to listen on 3000
EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# copying build from nodejs app to nginx location so that nginx can serve
COPY --from=builder /app/build /usr/share/nginx/html