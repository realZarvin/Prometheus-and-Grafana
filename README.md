
# Rust App Monitoring with Prometheus and Grafana

## Overview

This repository demonstrates an advanced monitoring and alerting setup using Prometheus and Grafana for a Rust application. The Rust application exposes metrics which are scraped by Prometheus, and these metrics are visualized and monitored using Grafana dashboards and alerts.

## Features

- **Rust Application**: A simple web application built with Actix-web that exposes Prometheus metrics.
- **Prometheus**: Scrapes and stores metrics from the Rust application.
- **Grafana**: Visualizes the metrics and sets up alerts based on defined thresholds.
- **Docker Compose**: Orchestrates the Rust application, Prometheus, and Grafana.

## Prerequisites

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Setup

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone <repository-url>
cd <repository-directory>


### 2. Build and Run the Docker Containers

Use Docker Compose to build and run the services:

```bash
docker-compose up --build
```

This command will build the Docker image for the Rust application and start the Rust application, Prometheus, and Grafana services.

### 3. Accessing the Services

- **Grafana**:
  - Open your browser and go to `http://localhost:3000`.
  - Log in with the default credentials (`admin` / `admin`).
  - Grafana will prompt you to change the default password.

- **Prometheus**:
  - Open your browser and go to `http://localhost:9090`.

- **Rust Application**:
  - Open your browser and go to `http://localhost:8000`.

## Project Structure

```
.
├── docker-compose.yml           # Docker Compose configuration file
├── prometheus.yml               # Prometheus configuration file
├── grafana                      # Grafana provisioning files
│   ├── datasource.yml           # Grafana datasource configuration
│   ├── dashboard.yml            # Grafana dashboard provisioning configuration
│   └── dashboards               # Directory for Grafana dashboards
│       └── rust-app-dashboard.json  # Grafana dashboard JSON
└── rust_app                     # Rust application directory
    ├── Cargo.toml               # Rust dependencies file
    ├── Cargo.lock               # Rust lock file
    ├── src
    │   └── main.rs              # Rust application source code
    └── Dockerfile               # Dockerfile for building the Rust application
```

## Rust Application Details

The Rust application is built using Actix-web and Prometheus crates. It exposes two endpoints:
- `/`: Increments a counter and returns "Hello, world!".
- `/metrics`: Exposes the Prometheus metrics.

### Running the Rust Application Locally

If you want to run the Rust application locally without Docker:

1. **Install Rust**: Follow the instructions on [rust-lang.org](https://www.rust-lang.org/learn/get-started).

2. **Run the Application**:

    ```bash
    cd rust_app
    cargo run
    ```

3. **Access the Application**:
    - Open your browser and go to `http://localhost:8000` to access the application.
    - Go to `http://localhost:8000/metrics` to see the metrics.

## Grafana Dashboard

The Grafana dashboard is pre-configured to visualize the total number of requests handled by the Rust application. The dashboard can be accessed and customized by following these steps:

1. Open Grafana in your browser at `http://localhost:3000`.
2. Navigate to the "Rust App Dashboard".
3. Customize the dashboard as needed.

## Prometheus Configuration

The Prometheus configuration file `prometheus.yml` specifies the scraping targets. It is set to scrape the Rust application's metrics from `rust_app:8000`.

### Customizing Prometheus

To customize Prometheus scraping intervals or add more targets, modify the `prometheus.yml` file and restart the Docker containers.

## Setting Up Alerts in Grafana

To set up alerts in Grafana:

1. Open the Grafana dashboard for the Rust application.
2. Edit the panel you want to add an alert to.
3. Navigate to the "Alert" tab and configure the alert conditions.
4. Save the dashboard.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.


## Conclusion

This detailed `README.md` file should provide clear instructions and information for anyone looking to set up and use the advanced monitoring and alerting system for the Rust application using Prometheus and Grafana.
