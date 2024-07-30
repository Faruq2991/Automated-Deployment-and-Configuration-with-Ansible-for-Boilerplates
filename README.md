# README

## Overview
This Ansible playbook configures a server and deploys a boilerplate Java web application. It sets up necessary directories, users, dependencies, and services, including PostgreSQL, RabbitMQ, Redis, Nginx, and a custom application service. The deployment includes setting up a virtual environment, installing dependencies, building the application, and configuring a reverse proxy with Nginx.

## Prerequisites
- Ansible installed on the control machine
- Target hosts accessible via SSH
- Sudo privileges for the Ansible user

## Variables
- **repository_url**: URL of the Git repository for the application.
- **branch**: Branch of the repository to deploy.
- **deploy_dir**: Directory where the application will be deployed.
- **pg_admin_user**: PostgreSQL admin username.
- **pg_admin_password**: PostgreSQL admin password.
- **pg_password_file**: Path to store PostgreSQL credentials.
- **app_port**: Port the application will run on.
- **nginx_port**: Port Nginx will listen on.
- **log_dir**: Directory for application logs.
- **log_error**: Error log file name.
- **log_out**: Output log file name.
- **hng_user**: System user for running the application.

## Tasks

1. **User Setup**: Creates a user (`hng`) and adds it to the sudoers file with no password required for sudo commands.

2. **Directory Creation**: Creates necessary directories for deployment, logging, and storing secrets.

3. **Git Configuration**: Configures Git to allow operations in all directories.

4. **Repository Cloning**: Clones the specified Git repository into the deployment directory.

5. **Ownership Configuration**: Sets ownership of the deployment directory to the application user.

6. **Dependency Installation**: Installs system packages including Python, PostgreSQL, RabbitMQ, Redis, Nginx, Maven, and OpenJDK.

7. **PostgreSQL Configuration**:
   - Configures PostgreSQL to use `md5` authentication for local and IPv6 connections.
   - Sets the password for the `postgres` user.
   - Creates a PostgreSQL database named `mydatabase`.
   - Saves PostgreSQL credentials to a specified file.

8. **Virtual Environment**: Creates a Python virtual environment in the deployment directory.

9. **Application Build**: Uses Maven to build the Java application.

10. **Systemd Service Setup**: Configures a systemd service for the application and starts it.

11. **Nginx Configuration**: Sets up Nginx as a reverse proxy for the application.

12. **Log File Ownership**: Ensures the log files are owned by the `hng` user.

## Handlers
- **Restart Application**: Restarts the application service whenever triggered.
- **Restart Nginx**: Restarts Nginx whenever triggered.

## Usage
1. Update the variables section with appropriate values.
2. Run the playbook using Ansible:
   ```bash
   ansible-playbook main.yaml -b
   ```
   
## Note
- Ensure the correct branch and repository URL are specified.
- Adjust file paths and system configurations as needed.
