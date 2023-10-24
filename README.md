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
   We will use the Docker-compose file and pull images of Prometheus and Grafana
   
2. **Node.js:**
   We will use the same Docker-compose file to build a Docker container serving the app
