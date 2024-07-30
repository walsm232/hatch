FROM node:18-alpine AS builder

WORKDIR /app

COPY ../hatch/package*.json ./

RUN npm install

COPY ../hatch ./

RUN npm run build



# Start of the resulting final image
# No credentials should be used beyond this point
FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
