# Stage 1: Build Environment
FROM node:18.17.0 AS build

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Clear npm cache and install dependencies
RUN npm install -g npm@10.9.0
RUN npm cache clean --force && npm install --legacy-peer-deps --force

# Copy the rest of your application code
COPY . .

# Build the application (if applicable)
RUN npm run build

# Stage 2: Production Environment
FROM node:18.17.0 AS production

# Set the working directory
WORKDIR /usr/src/app

# Copy only the necessary files from the build stage
COPY --from=build /usr/src/app/src ./src
COPY package*.json ./

# Clean npm cache before installing production dependencies
RUN rm -f package-lock.json
RUN npm cache clean --force

# Install only production dependencies
RUN npm install --omit=dev --legacy-peer-deps --force

# Expose the application port (adjust as necessary)
EXPOSE 3000

# Command to run your application
CMD ["node", "./src/index.js"]

