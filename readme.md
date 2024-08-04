 WordPress with MySQL and phpMyAdmin using Docker Compose

This project sets up a WordPress environment with a MySQL database and phpMyAdmin for database management using Docker Compose.

## Prerequisites

- Docker installed on your machine
- Docker Compose installed on your machine

## Directory Structure

Ensure your project directory structure looks like this:

my-wordpress-site/
├── docker-compose.yml
└── README.md


## Docker Compose Configuration

Create a file named `docker-compose.yml` in the root of your project directory with the following content:

```yaml
version: '3.8'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    image: wordpress:latest
    depends_on:
      - db
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    depends_on:
      - db
    ports:
      - "8080:80"
    restart: always
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: example

volumes:
  db_data:
  wordpress_data:



Getting Started
Follow these steps to get the WordPress environment up and running:



Start the services using Docker Compose:


docker-compose up -d
Verify the setup:

Open your browser and navigate to http://localhost:8000 to access the WordPress installation page.
Navigate to http://localhost:8080 to access phpMyAdmin.
Stopping the Services
To stop the services, run:


docker-compose down
Persisting Data
The defined volumes (db_data and wordpress_data) ensure that data persists even if the containers are removed. The data is stored on your local machine, allowing you to start the containers again without losing data.

Troubleshooting
If you encounter any issues, check the logs of the services for more details:


docker-compose logs db
docker-compose logs wordpress
docker-compose logs phpmyadmin
Additional Notes
Ensure Docker and Docker Compose are correctly installed and running on your machine.
Adjust environment variables and ports as necessary to fit your setup.
License
This project is licensed under the MIT License.



This `README.md` is formatted for a GitHub project and includes all the necessary steps and instructions to set up and run a WordPress, MySQL, and phpMyAdmin environment using Docker Compose. Make sure to adjust the repository URL and any other specific details to fit your project.





