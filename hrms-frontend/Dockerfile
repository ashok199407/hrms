# Use the official Node.js image as the base image
FROM node:18 As builder

# Set the working directory inside the container
WORKDIR /usr/src/app

# Install Angular CLI globally with the specified version
RUN npm install -g @angular/cli@latest

# Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Install project dependencies
#RUN npm install filepond
RUN npm install
#RUN npm audit fix --force
# Stage-2 
FROM node:18-slim AS runtime 

#copy packages
COPY --from=builder /usr/src/app/node_modules/ /usr/src/app/node_modules/

#copy entaire code
COPY . .
# Expose the port that the Angular app will run on
EXPOSE 4200

# Start the Angular application
CMD ["ng", "serve", "--host", "0.0.0.0"]


