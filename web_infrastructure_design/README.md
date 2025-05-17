
# Web Infrastructure Evolution Diagrams

This repository contains PlantUML diagrams representing the evolution of a web infrastructure for the website `www.foobar.com`. The diagrams illustrate different stages of the infrastructure, highlighting the components involved and the rationale behind each stage.

## Diagram 1: One-Server Web Infrastructure

### Components
- **Domain**: `www.foobar.com` (A record pointing to `8.8.8.8`)
- **Server**:
  - Nginx (web server)
  - Application server
  - Application files
  - MySQL database

### Purpose
This basic setup hosts the website on a single server, handling all web, application, and database functions.

### Issues
- **Single Point of Failure (SPOF)**: If the server goes down, the entire website becomes unavailable.
- **Downtime During Maintenance**: Restarting the web server or deploying new code causes downtime.
- **Scalability Limits**: One server cannot handle high traffic. No load balancing or redundancy.

## Diagram 2: Three-Server Web Infrastructure with Load Balancer

### Components
- **Domain**: `www.foobar.com`
- **Load Balancer (HAProxy)**: Round Robin, Active-Active setup
- **Backend Servers (2x)**:
  - Nginx (web server)
  - Application server
  - Application files
  - MySQL database (1 Primary, 1 Replica)

### Purpose
This setup adds load balancing and redundancy, distributing incoming traffic to multiple backend servers.

### Issues
- **Load Balancer SPOF**: If the load balancer fails, no traffic reaches the backend.
- **Single MySQL Write Node**: If the Primary fails, no writes can occur.
- **No Security or Monitoring**: Lacks firewalls, HTTPS, and monitoring.

## Diagram 3: Secure and Monitored Three-Server Infrastructure

### Components
- **Domain**: `www.foobar.com` (served over HTTPS)
- **Load Balancer (HAProxy)**: SSL termination
- **Firewalls (3x)**: One per server
- **Backend Servers (3x)**:
  - Nginx (web server)
  - Application server
  - Application files
  - MySQL database (1 Primary, 2 Replicas)
  - Monitoring agents (e.g., Sumo Logic)

### Purpose
This setup enhances security (firewalls, HTTPS) and observability (monitoring).

### Issues
- **SSL Termination at Load Balancer**: Exposes internal traffic to potential interception.
- **Single MySQL Write Node**: If the Primary fails, no writes can occur.
- **Identical Server Roles**: All-in-one servers reduce flexibility and scalability.

## Diagram 4: Split Components with Load Balancer Cluster

### Components
- **Domain**: `www.foobar.com`
- **Load Balancer Cluster (HAProxy)**: Configured as a cluster for high availability
- **Servers**:
  - **Web Server**: Nginx
  - **Application Server**: Application logic and files
  - **Database Server**: MySQL (Primary-Replica setup)

### Purpose
This setup splits components into dedicated servers, improving scalability and manageability.

### Explanation of Components
- **Load Balancer Cluster**: Distributes traffic and provides high availability.
- **Web Server**: Handles HTTP requests and serves static content.
- **Application Server**: Processes business logic and dynamic content.
- **Database Server**: Manages persistent data storage with redundancy.

### Issues
- **SPOF**: Load balancer cluster mitigates this, but individual server failures can still impact functionality.
- **Security**: Requires proper firewall rules and HTTPS configuration.
- **Monitoring**: Essential for proactive issue detection and resolution.

---

## Conclusion

These diagrams illustrate the evolution of a web infrastructure from a basic single-server setup to a more robust, secure, and scalable architecture. Each stage addresses specific issues and improves upon the previous design, ultimately leading to a more resilient and manageable system.

Feel free to explore the PlantUML code for each diagram and adapt it to your needs.
