# Node Container

# ! Use .dockerignore

# Use Red Hat UBI 9 as the base image
FROM redhat/ubi9-minimal:latest

ENV NODE_ENV=production

# Host port. The port that is exposed by the application on the server. Change accordingly.
ENV PORT=3000

# Install Node & npm
RUN microdnf install -y nodejs npm && \
    microdnf clean all

# Create a non-root user and switch to it (Change user name and UID as needed)
RUN useradd -r -u 1001 rwapps

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci --omit=dev && \
    npm cache clean --force

COPY . .

USER 1001

EXPOSE $PORT

CMD ["node", "server.js"]

# To build this image: "docker build -t <user_name>/<image_name>:<version> ."
# To build and push for multiple architectures: "docker buildx build   --platform linux/amd64,linux/arm64   -t <user_name>/<image_name>:<version>   --push ."

# To tag this image: "docker tag <image_name>:<version> <user_name>/<image_name>:<version>"

# To run this: "docker run -d --restart always -p <host_port>:<container_port> --name <app_name> <user_name>/<image_name>:<version>"
# To run this with .env: "docker run -d --restart always -p <host_port>:<container_port> --env-file .env --name <app_name> <user_name>/<image_name>:<version>"

# Default port for Spring Boot: 3000