# Docker Homework Solution

This document explains the step-by-step solution for the Docker homework assignment, which involves creating a Dockerfile and using Docker Compose to manage a multi-container application.

## Task 1: Write a Dockerfile

### Step 1: Create the Dockerfile

We create a `Dockerfile` that uses the official Nginx image as a base and adds our custom `index.html` file.

```dockerfile
# Use the official nginx image as the base image
FROM nginx:latest

# Copy the index.html file to the container
COPY index.html /usr/share/nginx/html/

# Expose port 80
EXPOSE 80
```

### Step 2: Create the index.html file

We create a simple `index.html` file with some basic content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Docker Homework</title>
</head>
<body>
    <h1>Hello from Docker!</h1>
    <p>This is a simple web page served by Nginx in a Docker container.</p>
</body>
</html>
```

### Step 3: Build and Run the Docker Image

To build and run the Docker image:

1. Save both the `Dockerfile` and `index.html` in the same directory.
2. Open a terminal and navigate to this directory.
3. Build the Docker image:
   ```
   docker build -t my-nginx-app .
   ```
4. Run the container:
   ```
   docker run -d -p 8080:80 my-nginx-app
   ```

After running these commands, you can access the web page at `http://localhost:8080`.
![image](https://github.com/user-attachments/assets/23224677-d9d3-41e4-9467-9604bcd6a524)



## Task 2: Run Multi-Container Application Using Docker Compose

### Step 1: Create the docker-compose.yml file

We create a `docker-compose.yml` file to define and run both the Nginx and Redis containers:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "8080:80"
    depends_on:
      - redis
  redis:
    image: "redis:alpine"
    ports:
      - "6379:6379"
```

### Step 2: Run the Multi-Container Application

To run the multi-container application:

1. Save the `docker-compose.yml` file in the same directory as your `Dockerfile` and `index.html`.
2. Open a terminal and navigate to this directory.
3. Run the following command:
   ```
   docker-compose up -d
   ```

This command starts both the web and Redis containers in detached mode.

### Step 3: Verify the Running Containers

![image](https://github.com/user-attachments/assets/657d9f38-d980-4d0a-be5a-8836692e3d10)


To verify that both containers are running:

1. Open a terminal.
2. Run the following command:
   ```
   docker ps
   ```

This will display a list of running containers, which should include both your Nginx web server and the Redis container.

