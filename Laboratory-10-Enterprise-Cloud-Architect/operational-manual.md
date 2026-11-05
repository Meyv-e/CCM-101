# CLOUDNOVA TECHNOLOGIES

## Enterprise Cloud Operational Manual

## 1. Project Overview

CloudNova Technologies is a private cloud environment developed as part of a Cloud Computing laboratory project. The infrastructure is deployed using Oracle VirtualBox, Ubuntu Server, Docker, and Docker Compose.

The project demonstrates how virtualization and containerization technologies can be used to deploy, manage, and maintain a web-based application within a private cloud environment.

The system hosts a WordPress website connected to a MariaDB database. WordPress serves as the web application platform, while MariaDB provides database storage and management.

CloudNova aims to demonstrate the practical implementation of cloud computing concepts, including virtualization, containerization, networking, persistent storage, application deployment, security, backup automation, and infrastructure maintenance.

The project provides an environment where users can understand how cloud infrastructure components work together to deliver application services.

## 2. System Architecture
- Host Operating System: Windows
- Hypervisor: Oracle VirtualBox
- Guest Operating System: Ubuntu Server
- Container Platform: Docker
- Web Application: WordPress
- Database: MariaDB

### 2.1 Infrastructure Overview

CloudNova Technologies follows a virtualized and containerized infrastructure model. The system uses a Windows computer as the host operating system, Oracle VirtualBox as the hypervisor, and Ubuntu Server as the guest operating system.

Ubuntu Server serves as the primary environment for hosting and managing Docker containers. Docker provides the containerization platform, while Docker Compose simplifies the deployment and management of multiple application services.

The infrastructure is composed of the following components:

- **Host Operating System:** Windows provides the physical computing environment.
- **Hypervisor:** Oracle VirtualBox manages the virtual machine.
- **Guest Operating System:** Ubuntu Server provides the Linux environment for cloud services.
- **Container Platform:** Docker manages application containers.
- **Container Management:** Docker Compose manages the application services.
- **Web Application:** WordPress provides the website interface.
- **Database Management System:** MariaDB stores application data.

### 2.2 Virtualization Layer

Oracle VirtualBox is responsible for creating and managing the Ubuntu Server virtual machine.

Virtualization allows the project to run a separate operating system without requiring an additional physical computer.

Ubuntu Server operates independently within the virtual machine while sharing the physical hardware resources of the Windows host.

This approach provides flexibility in configuring the cloud environment and allows administrators to manage the server without affecting the host operating system.

### 2.3 Containerization Layer

Docker is used to run WordPress and MariaDB as separate containers.

Containerization allows applications and their dependencies to operate in isolated environments. This improves application organization and simplifies deployment.

Docker Compose manages the relationship between the WordPress and MariaDB services through a centralized configuration file.

The use of containers makes it easier to start, stop, restart, and maintain the application components.

### 2.4 Application and Database Layer

The WordPress container serves as the application layer of CloudNova.

It provides the website interface and processes user requests. WordPress communicates with MariaDB to retrieve and store website information.

The MariaDB container serves as the database layer. It stores website content, user information, settings, and other application data.

Both containers communicate through the internal Docker network, allowing the application to access the database without requiring direct external database access.

## 3. Network Configuration

### 3.1 Network Configuration Overview

The CloudNova environment uses a network configuration that allows users to access the WordPress application while maintaining internal communication between application services.

The Ubuntu Server provides the main network environment for the Docker containers.

The configured network information includes:

- Ubuntu Server IP Address: `192.168.5.101`
- WordPress Port: `8080`
- SSH Port: `22`
- MariaDB Port: `3306`
- Docker Network: `cloudnova`

### 3.2 WordPress Network Access

The WordPress website is accessed through the Ubuntu Server IP address and port 8080.

The configured website address is:

`http://192.168.5.101:8080`

The port allows incoming HTTP requests to reach the WordPress application.

Users connected to the appropriate network can access the website through a browser by entering the server's IP address and port.

The availability of the website depends on the Ubuntu Server network configuration, Docker container status, and firewall rules.

### 3.3 SSH Remote Administration

Secure Shell (SSH) is used to remotely access and administer Ubuntu Server.

SSH operates through port 22 and allows administrators to execute commands, manage files, monitor services, and perform maintenance remotely.

SSH access provides an efficient way to manage the server without requiring direct access to the VirtualBox console.

Only authorized users should be permitted to access the server through SSH.

### 3.4 Internal Docker Network

The Docker network named `cloudnova` enables communication between the WordPress and MariaDB containers.

The internal network allows WordPress to connect to the database using the database service name defined in the Docker Compose configuration.

This configuration separates internal application communication from external website access.

MariaDB does not need to be directly accessible from external devices for normal WordPress operation.

The internal network also helps organize application communication and reduces unnecessary database exposure.

## 4. Application Deployment

### 4.1 Deployment Overview

CloudNova uses Docker Compose to deploy the WordPress application and MariaDB database.

Docker Compose provides a centralized configuration for defining the containers, networks, environment variables, and persistent storage.

The application deployment process ensures that the WordPress and MariaDB services are configured to work together.

### 4.2 WordPress Container

The WordPress container provides the website functionality of CloudNova.

It processes incoming website requests and generates the appropriate responses.

The container communicates with MariaDB to retrieve application information and save changes to the website.

WordPress requires a functioning database connection to operate correctly.

### 4.3 MariaDB Container

The MariaDB container stores and manages the database information required by WordPress.

It provides database services to the WordPress application through the internal Docker network.

The database container is responsible for maintaining the website's persistent information.

The database should be protected from unnecessary external access to maintain the security and integrity of application data.

### 4.4 Starting the Application

To start the CloudNova application, execute the following command from the directory containing the Docker Compose configuration file:

```bash
sudo docker compose up -d
```

This command creates or starts the required containers and runs them in detached mode.

Detached mode allows the application to continue running in the background while the administrator uses the terminal for other tasks.

### 4.5 Checking Running Containers

To verify that the containers are running:

```bash
sudo docker ps
```

This command displays the currently running Docker containers, including their names, status, and published ports.

To display all containers, including stopped containers:

```bash
sudo docker ps -a
```

Administrators should confirm that both WordPress and MariaDB are running properly before accessing the website.

### 4.6 Restarting the Application

To restart the application services:

```bash
sudo docker compose restart
```

Restarting the services can help resolve temporary application issues.

However, persistent problems should be investigated through container logs and configuration checks.

### 4.7 Stopping the Application

To stop the application services:

```bash
sudo docker compose stop
```

This stops the containers without deleting them.

To start the stopped services again:

```bash
sudo docker compose start
```

### 4.8 Application Logs

Docker Compose provides access to application logs for monitoring and troubleshooting.

To view application logs:

```bash
sudo docker compose logs
```

To continuously monitor logs:

```bash
sudo docker compose logs -f
```

Logs help identify application errors, database connection problems, and container startup issues.

## 5. Persistent Storage

### 5.1 Storage Overview

Persistent storage is an important component of CloudNova because it ensures that application data remains available even when containers are stopped or recreated.

Docker volumes are used to store important information independently of the container lifecycle.

Without persistent storage, application data stored only inside a container's writable layer may be lost when the container is removed.

### 5.2 WordPress Persistent Storage

WordPress requires persistent storage for website files and uploaded content.

The storage may contain:

- Website themes
- Plugins
- Uploaded images
- Website files
- Application configuration

Persistent WordPress storage helps maintain website content during container recreation and application updates.

### 5.3 MariaDB Persistent Storage

MariaDB requires persistent storage to maintain database information.

The database volume contains the information necessary for WordPress to operate.

This includes website content, user information, and application settings stored within the database.

The database volume should be protected against accidental deletion and unauthorized access.

### 5.4 Docker Volume Management

To list available Docker volumes:

```bash
sudo docker volume ls
```

To inspect a specific volume:

```bash
sudo docker volume inspect volume_name
```

Administrators should verify that the expected volumes exist and are correctly associated with the application containers.

### 5.5 Storage Maintenance

Storage maintenance includes monitoring disk usage, checking volume availability, and ensuring that important data is backed up.

The following practices are recommended:

- Avoid deleting volumes without verifying their contents.
- Perform backups before major application changes.
- Monitor available disk space.
- Verify that WordPress and MariaDB volumes are correctly configured.
- Maintain separate backups of important application data.

## 6. Firewall Configuration

### 6.1 Firewall Overview

CloudNova uses UFW, also known as Uncomplicated Firewall, to manage network access on Ubuntu Server.

The firewall controls incoming and outgoing network traffic based on configured rules.

Firewall configuration is an important security measure because it helps prevent unauthorized access to server services.

### 6.2 Firewall Policies

The configured firewall policies include:

- Default incoming traffic: Denied
- Default outgoing traffic: Allowed
- SSH access: Port 22 allowed
- WordPress access: Port 8080 allowed

These policies allow required application services while restricting unnecessary incoming connections.

### 6.3 Firewall Rules

To allow SSH traffic:

```bash
sudo ufw allow 22/tcp
```

To allow WordPress traffic:

```bash
sudo ufw allow 8080/tcp
```

To deny incoming traffic by default:

```bash
sudo ufw default deny incoming
```

To allow outgoing traffic by default:

```bash
sudo ufw default allow outgoing
```

To enable UFW:

```bash
sudo ufw enable
```

SSH access should be allowed before enabling the firewall to avoid losing remote server access.

### 6.4 Firewall Status Verification

To check the current firewall configuration:

```bash
sudo ufw status verbose
```

This command displays the firewall status, configured rules, and default policies.

Administrators should verify that the required services are permitted and unnecessary ports remain restricted.

### 6.5 Docker Firewall Considerations

Docker-published ports may interact with firewall rules differently from ordinary Ubuntu services.

Docker can create network rules that affect how traffic is filtered. As a result, published container ports may not always follow ordinary UFW filtering behavior.

CloudNova administrators should verify Docker network exposure and ensure that only necessary services are accessible.

MariaDB should remain accessible only through the internal Docker network whenever possible.

## 7. Backup and Recovery

### 7.1 Backup Overview

CloudNova implements database backup automation to protect important application information.

The backup process uses a Bash script to create compressed MariaDB database backups.

Database backups are essential for protecting against accidental data loss, database corruption, application failures, and infrastructure problems.

### 7.2 Backup Directory

The configured backup directory is:

`/opt/cloudnova/backups`

The database backup files use the `.sql.gz` file extension.

This format represents an SQL database dump compressed using gzip.

Compression helps reduce the amount of storage required for backup files.

### 7.3 Manual Backup Execution

To execute the backup script manually:

```bash
sudo /opt/cloudnova/backup.sh
```

The script is designed to export the MariaDB database and store the compressed backup in the designated directory.

The backup process should include database export, compression, file storage, and basic error handling.

Administrators should verify that the script completes successfully and produces a valid backup file.

### 7.4 Backup Verification

To check the available backup files:

```bash
sudo ls -lh /opt/cloudnova/backups
```

To check the total backup directory size:

```bash
sudo du -sh /opt/cloudnova/backups
```

Backup verification helps confirm that the backup process is producing files and that sufficient storage is available.

### 7.5 Database Recovery

Database recovery restores previously backed-up information to MariaDB.

The recovery process should be performed carefully to avoid overwriting important existing data.

A typical recovery procedure includes:

1. Identify the required backup file.
2. Verify the backup file's availability.
3. Confirm that MariaDB is running.
4. Prepare the database for restoration.
5. Import the database backup.
6. Verify the recovered application.

Recovery should be tested in a controlled environment whenever possible.

### 7.6 Backup Protection

Backup files should be protected because they may contain sensitive website and database information.

Recommended practices include restricting access to backup directories, maintaining multiple recovery points, and storing additional backup copies outside the virtual machine.

## 8. Automation

### 8.1 Automation Overview

CloudNova uses Cron to automate database backup operations.

Cron is a Linux scheduling service that executes commands or scripts at specified times.

Automation improves operational efficiency by reducing manual intervention and ensuring that scheduled maintenance tasks are performed regularly.

### 8.2 Scheduled Database Backup

The database backup is configured to run daily at 10:00 PM.

The scheduled task executes the Bash backup script located at:

`/opt/cloudnova/backup.sh`

This automation helps maintain regular database backup copies.

### 8.3 Cron Configuration

To view the current user's Cron schedule:

```bash
crontab -l
```

To view the root user's Cron schedule:

```bash
sudo crontab -l
```

To edit the root user's Cron schedule:

```bash
sudo crontab -e
```

The following Cron entry represents a daily backup at 10:00 PM:

```cron
0 22 * * * /opt/cloudnova/backup.sh
```

The schedule follows the Ubuntu Server's configured local time.

### 8.4 Cron Service Monitoring

To check the Cron service status:

```bash
sudo systemctl status cron
```

To start the service:

```bash
sudo systemctl start cron
```

To enable Cron during system startup:

```bash
sudo systemctl enable cron
```

### 8.5 Automation Verification

Administrators should verify that the scheduled backup is executing correctly.

Verification includes checking the Cron service, reviewing backup logs if available, confirming the creation of backup files, and checking the integrity of the generated backups.

Automated processes should be monitored regularly to ensure their reliability.

## 9. Maintenance

### 9.1 Maintenance Overview

Regular maintenance is necessary to maintain the stability, security, and performance of CloudNova Technologies.

Maintenance activities include operating system updates, Docker container monitoring, application log inspection, storage management, firewall verification, and backup validation.

### 9.2 Operating System Maintenance

Ubuntu Server should be updated regularly to maintain system security and compatibility.

To update package information:

```bash
sudo apt update
```

To install available package updates:

```bash
sudo apt upgrade
```

Administrators should review important updates before installation because operating system changes may affect running applications or services.

### 9.3 Docker Maintenance

Docker containers should be monitored regularly to ensure that application services remain operational.

To check running containers:

```bash
sudo docker ps
```

To check container resource usage:

```bash
sudo docker stats
```

To inspect application logs:

```bash
sudo docker compose logs
```

These commands help identify resource limitations, application errors, and service interruptions.

### 9.4 Storage Maintenance

Storage usage should be monitored to prevent disk space exhaustion.

To check available disk space:

```bash
df -h
```

To check Docker volumes:

```bash
sudo docker volume ls
```

Administrators should ensure that sufficient storage is available for application files, database information, and backup files.

### 9.5 Network Maintenance

Network maintenance includes checking server connectivity, reviewing firewall rules, and verifying that application services are accessible.

The Ubuntu Server IP address should be verified when network problems occur.

Administrators should also confirm that the Docker network remains available and that WordPress can communicate with MariaDB.

### 9.6 Recommended Maintenance Activities

Regular maintenance should include:

- Checking application availability.
- Reviewing Docker container status.
- Verifying database backups.
- Monitoring system resource usage.
- Reviewing firewall configuration.
- Updating system packages.
- Inspecting application logs.
- Testing database recovery procedures.

These activities help maintain the reliability of the CloudNova infrastructure.

## 10. Troubleshooting

### 10.1 WordPress Website Unavailable

Possible causes include stopped containers, incorrect IP configuration, firewall restrictions, or network connectivity problems.

Administrators should verify that WordPress is running and that port 8080 is correctly configured.

Useful commands:

```bash
sudo docker ps
sudo docker compose logs wordpress
sudo ufw status
```

### 10.2 MariaDB Connection Problems

Database connection problems may occur because of incorrect credentials, stopped containers, or Docker network configuration issues.

Administrators should verify that MariaDB is running and that WordPress is configured to use the correct database service name.

Useful commands:

```bash
sudo docker ps
sudo docker compose logs mariadb
sudo docker network ls
```

### 10.3 Docker Container Startup Failure

Container startup failures may result from incorrect Docker Compose configuration, port conflicts, insufficient resources, or missing environment variables.

Useful commands:

```bash
sudo docker compose config
sudo docker compose logs
sudo docker ps -a
```

The error messages should be reviewed before attempting further configuration changes.

### 10.4 Backup Failure

Backup failures may occur because of incorrect database credentials, unavailable containers, insufficient storage, or missing backup directories.

Administrators should verify that the backup script has the necessary permissions and that MariaDB is available.

Useful commands:

```bash
sudo docker ps
sudo df -h
sudo ls -ld /opt/cloudnova/backups
```

### 10.5 Network Connectivity Issues

Network problems may prevent users from accessing the WordPress website.

Administrators should verify the Ubuntu Server IP address, VirtualBox network configuration, firewall rules, and Docker port mappings.

Network troubleshooting should begin by identifying whether the problem originates from the host system, virtual machine, container network, or application service.

## 11. Security Recommendations

### 11.1 Access Control

CloudNova should restrict administrative access to authorized users.

Strong passwords and appropriate access permissions should be used for Ubuntu Server, WordPress, and MariaDB.

SSH access should be limited to trusted users, and unnecessary administrative accounts should be avoided.

### 11.2 Database Security

MariaDB should not be exposed directly to external networks unless there is a specific requirement.

The database should communicate with WordPress through the internal Docker network.

Database credentials should be protected and should not be unnecessarily shared or included in public documentation.

### 11.3 System Security

The Ubuntu Server environment should receive regular security updates.

Administrators should review firewall policies, monitor system logs, and avoid running unnecessary services.

Docker and its related components should also be maintained to reduce potential security risks.

### 11.4 Backup Security

Database backups should be protected against unauthorized access.

The backup directory should have appropriate permissions, and additional backup copies should be stored securely.

Backup files should be periodically tested to ensure that they can be used for recovery.

## 12. Limitations and Future Improvements

### 12.1 Current Limitations

CloudNova demonstrates the essential concepts of private cloud infrastructure and containerized application deployment.

However, the current implementation may have limitations related to scalability, monitoring, security, and availability.

The environment depends on a single virtual machine, which may affect service availability if the host computer or virtual machine experiences problems.

The current backup implementation focuses on database protection and may require additional procedures to fully recover the entire application environment.

### 12.2 Future Enhancements

The CloudNova infrastructure may be improved through the following enhancements:

- Implementing HTTPS and SSL/TLS certificates.
- Adding a reverse proxy.
- Improving backup retention and cleanup automation.
- Storing backup copies outside the virtual machine.
- Implementing monitoring and alerting tools.
- Improving container security.
- Strengthening network isolation.
- Implementing automated recovery procedures.
- Improving system scalability and availability.

These enhancements can help improve the reliability, security, and maintainability of the project.

## 13. Conclusion

CloudNova Technologies demonstrates the implementation of a private cloud environment using virtualization, containerization, networking, application deployment, persistent storage, firewall configuration, and automated database backups.

The project integrates Oracle VirtualBox, Ubuntu Server, Docker, Docker Compose, WordPress, and MariaDB to create a functional multi-tier web application.

Through the implementation of this infrastructure, the project demonstrates practical knowledge of cloud computing technologies and server administration.

The operational procedures included in this manual provide guidance for deploying, managing, monitoring, securing, and maintaining the CloudNova environment.

CloudNova Technologies serves as a foundation for further improvements in infrastructure automation, security, scalability, monitoring, and cloud operations.
