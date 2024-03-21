# Stage 1: Build Angular application
FROM node:18-alpine AS build

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
FROM node:18-alpine AS serve

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy built Angular app from previous stage
COPY --from=build /usr/src/app/dist/ /usr/src/app/dist/

# Expose port 4200 to serve the Angular app
EXPOSE 4200

# Start the Angular application
CMD ["npx", "http-server", "dist", "-p", "4200"]


