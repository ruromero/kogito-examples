# DMN + Spring Boot example

## Description

A simple DMN service to evaluate a traffic violation.

## Installing and Running

### Prerequisites

You will need:
  - Java 11+ installed
  - Environment variable JAVA_HOME set accordingly
  - Maven 3.6.2+ installed

### Compile and Run

```sh
mvn clean compile spring-boot:run
```

### Package and Run

```sh
mvn clean package
java -jar ./target/dmn-springboot-example.jar
```

## Example Usage

Once the service is up and running, you can use the following example to interact with the service.

### POST /Traffic Violation

Returns penalty information from the given inputs -- driver and violation:
Given inputs:

```json
{
    "Driver":{ "Points":2 },
    "Violation":{
        "Type":"speed",
        "Actual Speed":120,
        "Speed Limit":100
    }
}
```

Curl command (using the JSON object above):

```sh
curl -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' -d '{"Driver":{"Points":2},"Violation":{"Type":"speed","Actual Speed":120,"Speed Limit":100}}' http://localhost:8080/Traffic%20Violation
```

As response, penalty information is returned.

Example response:
```json
{
  "Violation":{
    "Type":"speed",
    "Speed Limit":100,
    "Actual Speed":120
  },
  "Driver":{
    "Points":2
  },
  "Fine":{
    "Points":3,
    "Amount":500
  },
  "Should the driver be suspended?":"No"
}
```


## Deploying with Kogito Operator

In the [`operator`](operator) directory you'll find the custom resources needed to deploy this example on OpenShift with the [Kogito Operator](https://docs.jboss.org/kogito/release/latest/html_single/#chap_kogito-deploying-on-openshift).

