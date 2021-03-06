## SpringBoot app with monitoring
- CREDIT: https://github.com/thbrunzendorf/monitoring-demo
## Setup
- Docker
- JDK8
- maven

## Stack
- SpringBoot
- prometheus
- promtail
- loki
- grafana
- Jaeger

## How to run ?

1. Fire up Docker

2. Run project as is. REST endpoint should be up.
    - POST: localhost:8080/api/cal  
    `{"op": "P", "left": "3", "right": "4"}`
    - GET:  localhost:8080/api/mov

    - GET localhost:8080/fib/9
    this require a separate "microservice" to help solve fibonacci number
    https://github.com/victorlee0505/DummySpring.git (run this app as is.)
    to simulate call stack and tracable by jaeger

3. under project root
    $ cd docker
    $ docker-compose up

4. Done.

## What can i do?
This stack has multiple services

- access Prometheus: http://localhost:9090 , in `Expression` search for log4j2_events_total and execute
- access Promtail: http://localhost:9080/ready , you should see `Ready`.
- access Loki: http://localhost:3100/metrics , http://localhost:3100/loki/api/v1/query?query=%7Bjob=%22spring-app%22%7D

The services above are used by Grafana to visualize data.

## GUI

- access Jaeger: http://localhost:16686/
    This is where you can trace a distributed service (group of microservices)(GET localhost:8080/fib/9)

This is where Grafana is used
- acess Grafana GUI: http://localhost:3000/
    login: admin, admin

    you should see 2 Dashboards.

- in Discover, you can pick different datasource, try choose jaeger, you will see something similar to jaeger UI.
