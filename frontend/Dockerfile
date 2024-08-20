# STAGE 1 - Base Image
FROM node:18-alpine AS base
WORKDIR /app
COPY package.json ./
RUN npm install

# STAGE 2 - Development Stage 
FROM base AS development
COPY . .
EXPOSE 3000
CMD ["npm", "run", "dev"]

# STAGE 3 - Build Stage
FROM base AS build
COPY . .
RUN npm run build

FROM node:18-alpine AS production
WORKDIR /app
RUN npm i -g serve
COPY --from=build /app/dist ./dist
EXPOSE 3000
CMD ["serve", "-s", "dist"]

# inspect container files - docker exec -it c821ed26477e /bin/sh
# c821ed26477e - as container ID

# then
# ls app to check directortory