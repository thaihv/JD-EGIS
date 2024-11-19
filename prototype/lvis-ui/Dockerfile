FROM node:20.16.0

WORKDIR /app
COPY package*.json ./

# Install dependencies and build the app
RUN npm install
RUN npm run build

# Use the official Nginx image to serve the built React app
FROM nginx:alpine

# Copy custom Nginx configuration
COPY nginx/nginx.conf /etc/nginx/nginx.conf

# Copy React build output to Nginx's default HTML directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 8086
EXPOSE 8086

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]