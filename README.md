# Django Nginx Deployment

This repository contains the code and instructions for deploying a Django app with Nginx as a reverse proxy on an EC2 Ubuntu instance.

## Prerequisites

Before getting started, ensure that you have the following prerequisites installed on your EC2 Ubuntu instance:

- Nginx
- Docker

## Deployment Steps

Follow these steps to deploy the Django app on the EC2 instance:

1. Update the package list and install Nginx:
   ```bash
   sudo apt-get update
   sudo apt install nginx -y

2. Restart Nginx:
    ```bash
    sudo systemctl restart nginx

3. Clone the Django app repository:
    ```bash
    git clone https://github.com/ameyapb/django-nginx-deployment.git

4. Install Docker and add the current user to the docker group:
    ```bash
    sudo apt install docker.io
    sudo usermod -aG docker $USER
    sudo reboot

5. Build the Docker image for the app:

    ```bash
    cd django-nginx-deployment/
    docker build -t notes-app .

6. Run the Docker container:

    ```bash
    docker run -d -p 8000:8000 notes-app:latest
  
7. Configure Nginx as a reverse proxy:

    ```bash
    sudo vim /etc/nginx/sites-enabled/default
    In the default configuration file, update the Nginx location block to proxy requests to the app running on localhost:8000.

8. Restart Nginx:
    ```bash
    sudo systemctl restart nginx

9. Copy static files to the web server's root directory:

    ```bash
    sudo cp -r ~/django-nginx-deployment/mynotes/build/* /var/www/html/

## Usage

To access the deployed Django app, open a web browser and enter the public IP address of your EC2 instance.
