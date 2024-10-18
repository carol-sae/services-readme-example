# **Service name**

_Include CircleCI status and SonarCloud badges for health check. For example:_

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/RedTecLab/order-service/tree/master.svg?style=svg&circle-token=395596542bf40c435c3b3145f42017ceed5f3466)](https://dl.circleci.com/status-badge/redirect/gh/RedTecLab/order-service/tree/master)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=vulnerabilities&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=bugs&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=com.redteclab%3Aorder-service&metric=code_smells&token=8f4ad9c7557e974f651590ee5d681e96768172ca)](https://sonarcloud.io/summary/new_code?id=com.redteclab%3Aorder-service)

#

_Include Tech Stack badges. For example:_

![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/Rabbitmq-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![CircleCI](https://img.shields.io/badge/circle%20ci-%23161616.svg?style=for-the-badge&logo=circleci&logoColor=white)
![Dependabot](https://img.shields.io/badge/dependabot-025E8C?style=for-the-badge&logo=dependabot&logoColor=white)![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)

Source: [markdown badges](https://github.com/Ileriayo/markdown-badges)

## **Description**

_Include a brief description of what the service does, its core functionality, and its main purpose. For example:_

The Order Service acts as a central service to store and process all order related information in the shop.

## **Table of Contents**

1. [Software Architecture](#software-architecture)
2. [Prerequisites](#prerequisites)
3. [Setup](#setup)
4. [Testing](#testing)
   - [Unit tests](#unit-tests)
   - [Integration tests](#integration-tests)
5. [Deployment](#deployment)
6. [Debugging](#debugging)
7. [Extras](#extras)
   - [API contract](#api-contract)
   - [RabbitMQ](#rabbitmq)
   - [Database ollection](#database-collection)
   - [Metrics](#metrics)
   - [Owners](#owners)

## Software Architecture

<img src="/docs/diagram_example.jpg" alt="diagram" title="diagram example"/>

The following diagram provides a high-level view of the architecture of the Order Service integration. Order service communicate with numerous external systems. More details can be found at this [wiki link](https://wiki.shop-apotheke.com/display/RTLDEV/1.+Order+Service+Integration).

## **Prerequisites**

Before you begin, ensure you have the following installed:

- **JDK** >= 8
- **Environment Variables:**
  - `GH_REGISTRY_USERNAME`: Username for the GitHub Container Registry
  - `GH_REGISTRY_TOKEN`: Personal Access Token for the GitHub Container Registry

_You can refer to the `.env.example` file for more details._

## **Setup**

To set up and run the microservice locally, follow these steps:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/RedTecLab/service.git
   cd service
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

## **Testing**

### Unit Tests

Run the unit tests using the following command:

```bash
mvn -P unit-test test
```

Unit tests cover the core functionality of the service, ensuring methods and business logic are functioning as expected.

### Integration Tests

> The tests can be found at `src/test/java/integration`

Run the following commands from the project's root directory.

1. Prepare the Docker image for integration tests. This command builds the service's Docker image from scratch,
   ensuring all dependencies are up-to-date:

```
make prepare-integration-test
```

2. Run integration tests:

```
mvn -P integration-test test
```

## **Deployment**

1. CI/CD Pipeline: The deployment process is automated using CircleCI. Ensure all tests pass before deploying to production.
2. Manual Deployment: You can manually deploy the service using Docker:

```bash
docker-compose -f docker-compose.prod.yml up --build
```

## **Debugging**

To start debugging service locally

```bash
make start console
```

```bash
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005"
```

add remote debug configuration in intellij and specify remote port as 5006 i.e

<img width="1025" alt="Screenshot 2021-12-02 at 13 38 55" src="https://user-images.githubusercontent.com/40858198/144423805-43118f24-2a8e-4f9e-89d7-42fdf55e8cba.png">

## **Extras**

_Include any extra optional information. Below are some recommendation:_

### API Contract

https://github.com/RedTecLab/api/blob/master/contracts/order-service/v1.yaml

### RabbitMQ

This service interacts with RabbitMQ for processing order-related events. Include some information about.

### Database Collection

| Collection                          | Purpose                                                                                   |
| ----------------------------------- | ----------------------------------------------------------------------------------------- |
| orderDraftPaymentNotificationEvents | Stores all payment notifications received before an orderDraft was converted to an order. |
| orderUpdateEvents                   |                                                                                           |
| orderUpdateEventsHistory            |                                                                                           |

### Metrics

The service provides key performance metrics via a monitoring endpoint, such as:

- /metrics: Exposes Prometheus metrics for monitoring.
- [Grafana Dashboard](https://telemetry.fra1.sae.systems/grafana/d/WgleFec4k/f09f9ba0-efb88f-order-service?orgId=1&from=now-6h&to=now): Pre-configured to visualize service performance.

### Owners

Every service has an owner(s). Check out the codeowner file for reference.
