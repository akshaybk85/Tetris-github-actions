# Use the official Node.js 16 image as the base image
FROM node:16-slim AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) to the container
COPY package*.json ./

# Install project dependencies
RUN npm ci

# Copy the rest of the application code to the container
COPY . .

# Build the React app
RUN npm run build

# Use a lightweight web server to serve the built app
FROM nginx:stable-alpine

# Copy the built app from the builder stage to the nginx html directory
COPY --from=builder /app/build /usr/share/nginx/html

# Expose the port that the app will run on (usually 3000 by default)
EXPOSE 80

# Start the React app when the container starts
CMD [ "nginx", "-g", "daemon off;" ]
