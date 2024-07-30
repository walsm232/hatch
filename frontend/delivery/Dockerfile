FROM node:18-alpine AS builder

WORKDIR /app

COPY hatch/package*.json ./

RUN npm install

COPY hatch ./

RUN npm run build



# Start of the resulting final image
# No credentials should be used beyond this point!
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

COPY delivery/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
