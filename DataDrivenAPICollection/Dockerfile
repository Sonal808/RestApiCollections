# Use the official Node.js 20 image as the base image
FROM node:20

# Set the working directory in the container
WORKDIR /app

# Install Newman globally
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra

# Ensure the results directory exists
RUN mkdir -p /app/results

# Copy your Postman collection and environment files to the working directory
COPY DataDrivenAPIs.json .
COPY GoRestEnv.json .
COPY Testdata.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "DataDrivenAPIs.json", "-e", "GoRestEnv.json", "-d", "Testdata.csv", "-r", "cli,json,html,htmlextra", "--reporter-htmlextra-export", "/app/results/gorest.html"]
