FROM node:20-alpine AS build
ARG BUILD_ENV=production
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install
COPY . .
RUN yarn build:${BUILD_ENV}

FROM nginx:stable-alpine AS production
RUN addgroup --system --gid 1001 fullstack
RUN adduser --system --uid 1001 fullstack
RUN mkdir /app
COPY --from=build /app/build /app
COPY --chown=fullstack:fullstack nginx.conf /etc/nginx/nginx.conf
RUN chown fullstack:fullstack /app
USER fullstack
EXPOSE 8080
CMD ["nginx" , "-g" , "daemon off;"]
