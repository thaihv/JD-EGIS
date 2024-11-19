# Step 1: Build React app (Vite)
FROM node:20.16.0 AS build

WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of your app files
COPY ./src /app/src
COPY ./public /app/public
COPY . .

# Build the app using Vite (This should create the "dist" folder)
RUN npm run build
RUN ls -al /app/dist
# Step 2: Set up Nginx to serve the React app
FROM nginx:latest

# Copy custom Nginx configuration
COPY nginx/nginx.conf /etc/nginx/nginx.conf

# Copy the "dist" folder from the build stage to Nginx's html directory
COPY --from=build /app/dist /usr/share/nginx/html

# Debug: List files in the Nginx HTML directory
RUN ls -al /usr/share/nginx/html

# Expose the default port 80 for Nginx
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
