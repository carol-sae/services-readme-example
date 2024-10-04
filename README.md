# **Project Title**


_Include CircleCI status and SonarCloud badges. For example:_

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/RedTecLab/order-service/tree/master.svg?style=svg&circle-token=395596542bf40c435c3b3145f42017ceed5f3466)](https://dl.circleci.com/status-badge/redirect/gh/RedTecLab/order-service/tree/master)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=vulnerabilities&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=bugs&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=code_smells&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)


## **Description**

_A brief description of what the service does, its core functionality, and its main purpose. For example:_

The **Order Service** acts as a central service to store and process all order related information in the shop. 


## **Features**

_List features. For example:_
- **Order Management**: Create, update, delete, and retrieve orders.
- **Stock Validation**: Ensure product availability by validating with the Inventory Service before order creation.
- **Asynchronous Processing**: Processes background tasks using RabbitMQ (e.g., order confirmation emails).
- **Cache Layer**: Uses Redis for faster retrieval of order data.
- **API Documentation**: Automatically generated Swagger documentation for all endpoints.
- **Health Checks**: Provides health status of the service, including database and message broker connectivity.
- **Metrics**: Exposes Prometheus metrics for monitoring service performance.


---


## **Table of Contents**

1. [Prerequisites](#prerequisites)
2. [Setup](#setup)
3. [Tools](#tools)
4. [File structure](#file-structure)
5. [Testing](#testing)
   - [Unit tests](#unit-tests)
   - [Integration tests](#integration-tests)
6. [Deployment](#deployment)
7. [Debugging](#debugging)
8. [Extras](#extras)
   - [Metrics](#metrics)
   - [Health checks](#health-checks)


## **Prerequisites**
Before you begin, ensure you have the following installed:

- **JDK** >= 8
- **Environment Variables:**
  - `DATABASE_URL`: The URL for the database connection
  - `REDIS_HOST`: The Redis instance for caching
  - `RABBITMQ_URL`: URL for the RabbitMQ broker
  - `SERVICE_PORT`: The port where the service will run
  
_You can refer to the `.env.example` file for more details._


## **Setup**

To set up and run the microservice locally, follow these steps:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/RedTecLab/order-service.git
   cd order-service
    ```
2. **Install dependencies:**
    - Ensure you have Docker installed (or the required tools listed in the Tools section).
    - Run the application using Docker: 
    ```bash
    docker-compose up --build
    ```
3. **Set environment variables:**
    ```bash
    cp .env.example .env
    ```


## **Tools**

- Docker: Used for containerization and running the service in isolated environments.
- CircleCI: CI/CD tool for automating testing and deployments.
- SonarCloud: For code quality checks, including bugs, vulnerabilities, and code smells.


## **File Structure**

Here’s an overview of the major files and directories in this project:

```bash
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com/redteclab/orderservice  # Main application code
│   │   ├── resources
│   │       └── application.yml            # Service configuration
│   ├── test
│       ├── java
│       │   └── com/redteclab/orderservice  # Unit and integration tests
│       └── resources
├── Dockerfile                              # Docker container configuration
├── docker-compose.yml                      # Docker Compose for running multi-container environments
├── README.md                               # Project documentation
├── build.gradle                            # Gradle build script
└── .circleci                               # CircleCI configuration files for CI/CD
```


## **Testing**

### Unit Tests
Run the unit tests using the following command:
 ```bash
./gradlew test
 ```
 Unit tests cover the core functionality of the service, ensuring methods and business logic are functioning as expected.

### Integration Tests
To run integration tests:
 ```bash
./gradlew integrationTest
 ```
Integration tests ensure proper interaction between components such as the database, message broker (RabbitMQ), and caching (Redis).


## **Deployment**

1. CI/CD Pipeline: The deployment process is automated using CircleCI. Ensure all tests pass before deploying to production.
2. Manual Deployment: You can manually deploy the service using Docker:
 ```bash
docker-compose -f docker-compose.prod.yml up --build
 ```


## **Debugging**

For debugging the service locally, follow these steps:
- Logs: Access service logs by running:
 ```bash
docker logs order-service
 ```
 - Debug Mode: Run the service in debug mode by adding the DEBUG=true environment variable:
  ```bash
DEBUG=true docker-compose up
 ```
 

## **Extras**

### Metrics
The service provides key performance metrics via a monitoring endpoint, such as:
- /metrics: Exposes Prometheus metrics for monitoring.
- Grafana Dashboard: Pre-configured to visualize service performance.
 
### Health Checks
To monitor the health of the service, use:
- /health: Returns the overall health status of the microservice (e.g., database connectivity, queue availability).


## **License**
This project is licensed under the MIT License. See the LICENSE file for more details.
