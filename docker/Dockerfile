# Use an official Node.js runtime as the base image
FROM node:14 as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the React app
RUN npm run build

# Use an official NGINX image as the base image for serving the app
FROM nginx:alpine

# Copy the built app from the previous stage to the NGINX container
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom NGINX configuration if needed
# COPY docker/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 to the host
EXPOSE 80

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
