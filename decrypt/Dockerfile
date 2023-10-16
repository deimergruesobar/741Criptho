# Use the official NGINX image as the base image
FROM nginx

# Replace the default NGINX configuration with a custom configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Create a directory for the HTML file
WORKDIR /usr/share/nginx/html

# Download the decrypt.html file and save it as index.html
RUN apt-get update && apt-get install -y wget && \
    wget https://raw.githubusercontent.com/deimergruesobar/741Crypto/main/decrypt.html -O index.html && \
    apt-get remove --purge -y wget && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Expose port 8080
EXPOSE 8080

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]

