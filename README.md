

```markdown
# vprofile-project

## Overview

The `vprofile-project` sets up a multitier application stack using Docker containers. This stack includes Nginx (Web Server), Tomcat (Application Server), RabbitMQ (Broker/Queuing Agent), Memcache (DB Caching), and MySQL (SQL Database). Docker is used for containerizing each service, simplifying deployment and scaling.

## Prerequisites

1. **Docker**
   - Platform for developing, shipping, and running applications in containers.
   - [Download Docker](https://www.docker.com/products/docker-desktop)

2. **Docker Compose**
   - Tool for defining and running multi-container Docker applications.
   - [Install Docker Compose](https://docs.docker.com/compose/install/)

3. **Command Line Interface (CLI)**
   - Use your preferred CLI for running Docker commands.

4. **Integrated Development Environment (IDE)**
   - Used for editing Docker files and configuration.
   - Recommended: [Notepad++](https://notepad-plus-plus.org/downloads/)

## Architectural Design

The project utilizes the following Docker containers:
- **Nginx** - Web Server
- **Tomcat** - Application Server
- **RabbitMQ** - Broker/Queuing Agent
- **Memcache** - Database Caching
- **MySQL** - SQL Database

## Setup Instructions

1. **Clone the Repository**

   ```bash
   git clone https://github.com/devopshydclub/vprofile-project.git
   cd vprofile-project
   ```

2. **Configuration**

   Ensure you have the correct configuration in the `docker-compose.yml` and related Docker files.

3. **Build and Start Containers**

   ```bash
   docker-compose up --build
   ```

   This command will build the Docker images and start the containers defined in your `docker-compose.yml` file.

4. **Validate Containers**

   Check the status of your containers:

   ```bash
   docker ps
   ```

   You should see the containers for Nginx, Tomcat, RabbitMQ, Memcache, and MySQL running.

## Container Configuration

1. **MySQL Container**

   - Configuration: Defined in `docker-compose.yml`
   - Default password: `admin123`
   - Database name: `accounts`
   - User: `admin`

   Initialize the MySQL database:

   ```bash
   docker exec -it <mysql_container_name> mysql -u root -padmin123
   ```

   Run the following commands inside the MySQL container:

   ```sql
   CREATE DATABASE accounts;
   GRANT ALL PRIVILEGES ON accounts.* TO 'admin'@'%' IDENTIFIED BY 'admin123';
   FLUSH PRIVILEGES;
   ```

2. **Memcache Container**

   - Configuration: Defined in `docker-compose.yml`
   - Default port: `11211`

   To verify Memcache:

   ```bash
   docker exec -it <memcache_container_name> memcached-tool 127.0.0.1:11211 stats
   ```

3. **RabbitMQ Container**

   - Configuration: Defined in `docker-compose.yml`
   - Default user: `test`
   - Default password: `test`

   Access the RabbitMQ management interface:

   ```bash
   docker exec -it <rabbitmq_container_name> rabbitmqctl list_users
   ```

4. **Tomcat Container**

   - Configuration: Defined in `docker-compose.yml`
   - Default port: `8080`

   Deploy your application to Tomcat by placing your `.war` file in the `/usr/local/tomcat/webapps/` directory inside the container. 

   ```bash
   docker cp target/vprofile-v2.war <tomcat_container_name>:/usr/local/tomcat/webapps/ROOT.war
   ```

5. **Nginx Container**

   - Configuration: Defined in `docker-compose.yml`
   - Default port: `80`

   Ensure your Nginx configuration (`/etc/nginx/conf.d/default.conf` inside the container) correctly proxies requests to Tomcat.

## Code Build and Deployment

1. **Build Artifact**

   ```bash
   cd vprofile-project
   mvn install
   ```

   This command will build your application artifact (`vprofile-v2.war`).

2. **Deploy Artifact**

   Copy the built artifact to the Tomcat container:

   ```bash
   docker cp target/vprofile-v2.war <tomcat_container_name>:/usr/local/tomcat/webapps/ROOT.war
   ```

3. **Restart Containers**

   ```bash
   docker-compose restart
   ```

## Validation

1. **Verify Application**

   Get the IP address or hostname of your Docker host and access it via your browser. 

   For example, if you're using Docker Desktop, you can use `localhost` or `127.0.0.1`:

   ```http
   http://localhost
   ```

   Log in with `admin_vp` as both the username and password.

## License

Specify the license for your project here.

## Contact

For any questions or issues, please contact [Your Name](mailto:your-email@example.com).

```

Feel free to modify this template based on specific details or additional configurations in your Docker setup.
