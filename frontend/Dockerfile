FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

RUN if [! -d "/app/dist"]; then echo "build folder dist tidak ditemukan"; exit 1; fi

FROM node:18-alpine

WORKDIR /app

COPY --from=build /app/dist ./dist

RUN npm install -g http-server

EXPOSE 80

CMD ["http-server", "dist", "-p", "80"]
