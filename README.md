# Spring Boot Standalone App with Docker

A simple Spring Boot web application that displays a welcome page. The application is packaged with Maven and containerized with Docker, then can be run on an AWS EC2 instance.

## Technologies Used

- Java
- Spring Boot
- Maven
- Docker
- AWS EC2

## Project Features

- Serves a simple HTML welcome page from a Spring Boot REST controller.
- Builds the application as an executable JAR using Maven.
- Packages and runs the application in a Docker container.
- Supports host-to-container port mapping for access through a browser.

## Build the Application

Run from the project root:

```bash
mvn clean package
```

This generates the application JAR in the `target/` directory.

## Build the Docker Image

```bash
docker build -t standaloneapp .
```

## Run the Container

The Spring Boot application listens on port `8080` inside the container. This example exposes it on host port `8888`:

```bash
docker run -d -p 8888:8080 --name standalone-container standaloneapp
```

Open the application at:

```text
http://YOUR-EC2-PUBLIC-IP:8888/
```

Replace `YOUR-EC2-PUBLIC-IP` with the public IPv4 address of your EC2 instance. Make sure the instance's security group allows inbound TCP traffic on port `8888` from your IP address.

## Useful Docker Commands

```bash
docker ps
docker logs standalone-container
docker stop standalone-container
docker rm standalone-container
```

## Notes

- Keep private keys such as `.pem` files, credentials, and environment secrets out of GitHub.
- Generated Maven output in `target/` should not be committed.
- Do not expose application ports publicly unless needed; restrict security group access where possible.
