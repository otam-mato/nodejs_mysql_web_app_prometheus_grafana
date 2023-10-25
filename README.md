[the page is under revision]

# Node.JS + MySQL Web App.<br><br>Monitoring with Prometheus and Grafana.

<br>

> **Note:** This is a part of a series of demo projects in which I manipulate a Node.js application using various technologies.<br>
>
> The app built using Node.js and Express, originally presented at this [GitHub Repository](https://github.com/otam-mato/nodejs_mysql_web_app_terraform.git).
>
> In the current installment, I am setting up monitoring of the application using Prometheus and Grafana.
<br>

## Deployment Strategy

1. **Prometheus and Grafana Deployment:**
   We will use the Docker-compose file and pull images of Prometheus and Grafana from DockerHub
   
2. **Node.js:**
   We will use the same Docker-compose file to build a container, which will be serving the app

<br>

## Architecture Diagram

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/ec57c7b7-187f-410c-8edf-63d7e7a8314f" width="800px"/>
</p>

<br>

## Technologies used
- **Prometheus**
- **Grafana**
- **Node.JS**
- **Express**
- **JavaScript**
- **MySQL**
- **Docker, Docker-Compose**
- **AWS**
- **EC2**
<br>

## Functionality

This web application interfaces with a MySQL database, facilitating CRUD (Create, Read, Update, Delete) operations on the database records. Monitoring implemented via **Prometheus** and **Grafana**.

**<details markdown=1><summary markdown="span">Detailed app description</summary>**

## Summary

The app sets up a web server for a supplier management system. It allows viewing, adding, updating, and deleting suppliers. 

#### **Dependencies and Modules**:
   - **express**: The framework that allows us to set up and run a web server.
   - **body-parser**: A tool that lets the server read and understand data sent in requests.
   - **cors**: Ensures the server can communicate with different web addresses or domains.
   - **mustache-express**: A template engine, letting the server display dynamic web pages using the Mustache format.
   - **serve-favicon**: Provides the small icon seen on browser tabs for the website.
   - **Custom Modules**: 
     - `supplier.controller`: Handles the logic for managing suppliers like fetching, adding, or updating their details.
     - `config.js`: Keeps the server's settings for connectind to the MySQL database.

#### **Configuration**:
   - The server starts on a port taken from a setting (like an environment variable) or uses `3000` as a default.

#### **Middleware**:
   - It's equipped to understand data in JSON format or when it's URL-encoded.
   - It can chat with web pages hosted elsewhere, thanks to CORS.
   - Mustache is the chosen format for web pages, with templates stored in a folder named `views`.
   - There's a public storage (`public`) for things like images or stylesheets, accessible by anyone visiting the site.
   - The site's tiny browser tab icon is fetched using `serve-favicon`.

#### **Routes (Webpage Endpoints)**:
   - **Home**: `GET /`: Serves the home page.
   - **Supplier Operations**: 
     - `GET /suppliers/`: Fetches and displays all suppliers.
     - `GET /supplier-add`: Serves a page to add a new supplier.
     - `POST /supplier-add`: Receives data to add a new supplier.
     - `GET /supplier-update/:id`: Serves a page to update details of a supplier using its ID.
     - `POST /supplier-update`: Receives updated data of a supplier.
     - `POST /supplier-remove/:id`: Removes a supplier using its ID.

#### **Starting Up**:
   - The server comes to life, starts listening for visits, and announces its awakening with a log message.

</details>

**<details markdown=1><summary markdown="span">Prometheus details</summary>**

Prometheus is an open-source monitoring and alerting toolkit designed for reliability and scalability. It is part of the Cloud Native Computing Foundation (CNCF) and is widely used in the field of cloud-native and containerized applications. Prometheus is used for collecting, storing, and querying metrics and other essential data generated by various software systems.

Key features and components of Prometheus include:

1. **Data Collection**: Prometheus scrapes metrics from instrumented jobs, services, and applications at regular intervals. It supports multiple data formats, including a simple text-based format and more efficient binary formats.

2. **Data Storage**: Collected data is stored in a time-series database optimized for fast querying and aggregations. The database can be configured to retain data for a specified time.

3. **Query Language**: Prometheus Query Language (PromQL) allows users to write powerful queries to aggregate, transform, and process data for monitoring and alerting purposes.

4. **Alerting**: Prometheus supports alerting based on defined alerting rules. Alerts can be configured to notify operators or integrate with notification systems like Alertmanager.

5. **Scalability**: Prometheus is designed to be horizontally scalable, and it supports federated setups to collect and aggregate data from multiple Prometheus instances.

6. **Visualization**: While Prometheus itself doesn't provide visualization capabilities, it integrates well with other tools like Grafana for creating dashboards and visualizing data.

7. **Exporters**: Prometheus exporters are small applications or libraries that allow you to monitor various third-party systems, services, and components. Many popular software components have Prometheus exporters available.

Prometheus is often used in combination with other technologies such as Grafana for visualization and Alertmanager for alert management. It's especially popular in containerized and microservices-based environments, helping operators and developers monitor and troubleshoot complex, dynamic systems.

</details>

**<details markdown=1><summary markdown="span">Grafana details</summary>**

Grafana is an open-source, multi-platform analytics and monitoring platform designed to integrate with various data sources and provide advanced visualization, alerting, and exploration capabilities. It is commonly used in conjunction with time-series databases and monitoring systems, including Prometheus, InfluxDB, Elasticsearch, and more. Grafana allows users to create interactive and customizable dashboards to gain insights from their data.

Key features of Grafana include:

1. **Data Source Integration**: Grafana supports a wide range of data sources, including time-series databases (Prometheus, InfluxDB, Graphite), relational databases (MySQL, PostgreSQL), cloud services (AWS CloudWatch, Google Cloud Monitoring), and more. This versatility allows users to consolidate data from different systems in a single dashboard.

2. **Dashboard Creation**: Users can create dashboards to visualize and explore data through a web-based interface. Grafana offers a drag-and-drop dashboard builder with various panel types for different visualizations, such as graphs, tables, and maps.

3. **Data Querying**: Grafana provides an SQL-like query language for retrieving and manipulating data from data sources. Users can fine-tune queries and create custom transformations.

4. **Alerting**: Grafana supports alerting based on data queries and conditions. Users can configure thresholds and alert notifications, including email, Slack, and other channels, through integration with notification systems.

5. **Templating**: Templating enables the creation of dynamic dashboards. Variables can be used in queries and allow for easy switching between different data sources or filtering data.

6. **User and Team Management**: Grafana includes user authentication, role-based access control, and team management features, making it suitable for multi-user and collaborative environments.

7. **Plugins and Extensibility**: Grafana's plugin system allows for custom panels, data sources, and apps to be developed and integrated into the platform. This extensibility makes it adaptable to various use cases.

8. **Community and Community-Driven Development**: Grafana has an active and engaged open-source community, which results in frequent updates, a wide range of plugins, and community-contributed resources.

Grafana is widely used by DevOps, system administrators, and data analysts for monitoring infrastructure, applications, and services. It has become a standard tool for creating interactive, real-time dashboards that help users understand and respond to the performance and health of their systems.

</details>

<br>

## Prerequisites

- A work station or an **EC2** instance (I am using **Ubuntu 22.04**).
   
- <details markdown=1><summary markdown="span">Install Docker-compose, Node.js, npm, and Git </summary>
   <br>
   
   - **Install Docker-compose**

   ```
   sudo apt update
   sudo apt install docker-compose
   ```
   
   - **Install Node.js**

   ```
   sudo apt install nodejs
   ```
   
   - **Install npm**

   ```
   sudo apt install npm
   ```
   
   - **Install Git**

   ```
   sudo apt install git
   ```
   
  </details>

<br>

## Implementation

Follow these steps for successful implementation:

1. [**Modify the app files to allow Prometheus collecting metrics.**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#modify-the-app-files-to-employ-bunyan-for-logging)
2. [**Create the configuration file for Prometheus"prometheus.yml".**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#2-create-the-logstash-configuration-file)
4. [**Create the configuration file for Grafana "datasources.yml"**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#3-launch-the-elk-stack-with-this-docker-compose-file)
5. [**Create the Docker-compose file docker-compose.yml**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#4-to-employ-the-mysql-database-pull-and-run-this-image-from-dockerhub)
7. [**Launch the docker-compose.yml file**](https://github.com/otam-mato/nodejs_elk/blob/main/README.md#5-launch-the-app-and-click-a-few-times-at-any-links-to-start-producing-logs)

<br>

## Screenshots

<p align="center">
  <img src="https://github.com/otam-mato/nodejs_mysql_web_app_prometheus_grafana/assets/113034133/41b3ff50-2ef2-44f7-9bbf-eb8f875305dd" width="700px"/>
</p>


<p align="center">
  <img src="" width="700px"/>
</p>

<br>
