# Starting the App

To start the app, navigate to the project directory in your terminal and run the following command:

```bash
docker compose up --build
```

This will build the Docker image and start the container. You should see logs in your terminal indicating that the app is running.

To view the app, open your web browser and go to **[http://localhost:3000/](http://localhost:3000/)**

To stop the container, press **CTRL+C** in your terminal. To start the container again, run the same **docker compose up** command. When you're done with the app, you can remove the container with the following command:

```bash
docker compose down --remove-orphans
```

This will stop and remove the container, as well as any other containers that were created with **docker compose up**.

# Cleaning Up

To remove all containers, networks, and images that are not in use by any containers, you can run the following command:

```bash
docker system prune -a
```
This will free up disk space on your machine by removing any unnecessary Docker resources.

# Hot-Reload

Hot-reloading is a feature that allows you to see changes to your code in real-time without having to manually refresh your browser. To enable hot-reloading for your app, follow these steps:

## Step 1: Update package.json

In your project's **package.json** file, find the **"scripts"** section and update the **"start"** script as follows:

```json
"start": "WATCHPACK_POLLING=true react-scripts start",
```

This enables watch polling for hot-reloading.

## Step 2: Update Dockerfile

In your project's Dockerfile, set the working directory to /app and copy the project files into the container:

```Dockerfile
...
# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app/
...
```

## Step 3: Update docker-compose.yml

In your project's **docker-compose.yml** file, add the following lines to the **app** service:

```yml
services:
  app:
    ...
    # Set an environment variable to enable hot-reloading with nodemon
    environment:
      - CHOKIDAR_USEPOLLING=true
    # Mount the current directory as a volume in the container
    volumes:
      - .:/app
```

This sets an environment variable to enable hot-reloading with nodemon and mounts the current directory as a volume in the container.