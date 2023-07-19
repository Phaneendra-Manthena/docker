# Stage 1: Build the application using the Node.js base image
FROM node:14 AS build

# Create a non-root user with a home directory
RUN useradd -m myuser

# Set the working directory
WORKDIR /opt/server

# Copy the package.json and install dependencies as the non-root user
COPY package.json /opt/server/
RUN chown -R myuser:myuser /opt/server/
USER myuser
RUN npm install

# Copy the server.js file as the non-root user
COPY server.js /opt/server/

# Stage 2: Create the Distroless image and copy only necessary artifacts
FROM gcr.io/distroless/nodejs:14

# Set the working directory
WORKDIR /opt/server

# Copy the built application from the previous stage
COPY --from=build /opt/server /opt/server

# Set the entrypoint
CMD ["server.js"]
