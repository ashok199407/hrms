# Stage 1: Build the Node.js application
FROM node:18-slim AS build

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Install project dependencies
RUN npm install --only=production

# Copy the entire project to the container
COPY . .

# Build the Node.js application (if needed)
# RUN npm run build

# Stage 2: Create a lightweight runtime environment
FROM node:18-slim AS runtime

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy built Node.js application from the build stage
COPY --from=build /usr/src/app .

# Expose port (if applicable)
EXPOSE 3000

# Command to start the application
CMD ["ng", "serve", "--host", "0.0.0.0"]


