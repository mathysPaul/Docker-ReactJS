# Use the latest Node.js image as the base
FROM node:latest

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app/

# Install dependencies using npm
RUN npm install

# Set the default command to run when the container starts
CMD npm start