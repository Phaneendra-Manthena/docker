FROM node:14

# Create a non-root user with a home directory
RUN useradd -m myuser

# Set the working directory and expose the required port
WORKDIR /opt/server
EXPOSE 8080

# Copy the package.json and npm install as the non-root user
COPY package.json /opt/server/
RUN chown -R myuser:myuser /opt/server/
USER myuser
RUN npm install

# Copy the server.js file as the non-root user
COPY server.js /opt/server/

# Set the entrypoint
ENTRYPOINT ["node", "server.js"]
