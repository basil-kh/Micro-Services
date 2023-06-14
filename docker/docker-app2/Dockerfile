# Use an official Node.js runtime as the base image
FROM node:12

# label it - with your name
LABEL MAINTAINER=BASIL

# Set the working directory in the Docker container
WORKDIR /usr/src/app

# Clone your app from the repository
RUN git clone https://github.com/basil-kh/app.git .

# allow start.sh to be executed
RUN chmod +x start.sh

# Install the application dependencies
RUN npm install

# Expose port 3000 for the application
EXPOSE 3000

# Define the command to run the application
CMD ["./start.sh"]