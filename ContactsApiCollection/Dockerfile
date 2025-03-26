# Use the official Node.js 20 image as the base image
FROM node:20

# Set the working directory in the container
WORKDIR /app


# Install Newman globally
RUN npm install -g newman

#Install Newman html report
RUN npm install -g newman-reporter-html

#Install Newman Reporter HTMLExtra
RUN npm install -g newman-reporter-htmlextra

# Ensure the results directory exists
RUN mkdir -p /app/results


# Copy your Postman collection and environment files to the working directory
COPY ContactsAPI.json .
COPY ContactsEnv.json .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "ContactsAPI.json", "-e", "ContactsEnv.json", "-r", "cli,json,html,htmlextra", "--reporter-htmlextra-export", "/app/results/contactsTest.html"]