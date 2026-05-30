FROM node:20-alpine AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install
COPY . .

FROM node:20-alpine AS production
RUN addgroup --system --gid 1001 fullstack
RUN adduser --system --uid 1001 fullstack
WORKDIR /app
COPY --from=build /app/node_modules ./node_modules
COPY --chown=fullstack:fullstack server.js connect.js ./
COPY --chown=fullstack:fullstack handlers ./handlers
COPY --chown=fullstack:fullstack schemas ./schemas
ARG BUILD_ENV=production
COPY .env.${BUILD_ENV} .env
RUN chown -R fullstack:fullstack /app
USER fullstack
EXPOSE 5000
CMD ["node" , "server.js"]
