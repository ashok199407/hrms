# Stage 1: Build Angular application
FROM node:18 AS build

# Set the working directory inside the container
WORKDIR /usr/src/app

# Install Angular CLI globally with the specified version
RUN npm install -g @angular/cli@latest

# Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the entire project to the container
COPY . .

# Build the Angular application
RUN ng build 

# Stage 2: Serve Angular application
FROM nginx:latest

RUN rm -rvf /usr/share/nginx/html/*

# Copy built Angular app from previous stage
COPY --from=build /usr/src/app/dist/ /usr/share/nginx/html

# Expose port 80 to serve the Angular app
EXPOSE 80

# Start Nginx to serve the Angular app
CMD ["nginx", "-g", "daemon off;"]
