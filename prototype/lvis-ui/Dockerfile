FROM node:20.16.0 AS build

WORKDIR /app
COPY package*.json ./
COPY ./src /app/src
COPY ./public /app/public
COPY package.json package-lock.json /app/
COPY . .
# Install dependencies and build the app
RUN npm install
RUN npm run build

# Use the official Nginx image to serve the built React app
FROM nginx:alpine

# Copy custom Nginx configuration
COPY nginx/nginx.conf /etc/nginx/nginx.conf

# Copy React build output to Nginx's default HTML directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]