# kogito-avro-bug Project
This repo is a demo of an issue I've been experiencing between the Maven Avro plugin and Quarkus.

## Description of issue
When creating a BPMN process in Kogito, code generation fails with (1) the Avro Maven Plugin (2) a message node in the process
and (3) Certain output directory settings in the Avro Maven Plugin. 
The error is super cryptic: `java.lang.IllegalArgumentException: Cannot find method lambda$process$0[] on class...`

## Branches
- `main` - broken example with Message Node and Avro Maven Plugin (output dir set to `${project.build.directory}/generated-sources`)
- `working` - working process with Message Mode but no Avro Maven Plugin
- `working2` - working process with Avro Maven Plugin (output dir set to `${project.build.directory}/generated-sources`) but no Message Node
- `working3` - working process with Message Node and Avro maven plugin (output dir set to `src/main/java`)

## Running the application

Run (ensure you have Kafka running locally at `localhost:9092`)
```shell script
./mvnw compile quarkus:dev
```

Kick off my little test process
```shell
curl --location --request POST 'http://localhost:8080/test' \
--header 'Content-Type: application/json' \
--data-raw '{
	"message": "foobar"
}'
```
