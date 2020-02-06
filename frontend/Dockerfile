FROM alpine:3.7 AS builder

# Install base
RUN apk add --update nodejs nodejs-npm

# Set the directory we want to run the next commands for
WORKDIR /code
# Copy our source code into the container
COPY . .

# Build the app
RUN npm install && \
    npm build

##############################
##############################

FROM nginx

RUN npm install
RUN npm build

COPY --from=builder /code/public /var/www/html
COPY ./nginx.conf /etc/nginx/nginx.conf
WORKDIR /etc/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
