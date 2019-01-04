# Confluent Apache Kafka for Developers Course - Adapted

This is a fork of [confluentinc/training-developer-src](https://github.com/confluentinc/training-developer-src]) with the following enhancements:

1. It allows running the exercise examples in the ***host machine*** (not only within the openjdk docker container),
   especially directly in an IDE (*Eclipse*, *IntelliJ IDEA*).
1. All Java samples can be built also as ***Maven*** based projects (parallel to *Gradle*)

### Details for Enhancement 1

The following changes were made or have to be made

- The ports for the broker (`kafka`), the `schema-registry` and `rest-proxy` are also exposed to the host by a modification of `docker-compose.yml`.
- Additionally there is a code snippet for host machine's `/etc/hosts` file in [solution/hosts](solution/hosts). This has to be added **manually**.
  
### Details for Enhancement 2

The following projects are also available as Maven projects in parallel to Gradle:

- *basic-consumer*
- *basic-producer*
- *previous-data*
- *custom-partitioner*
- *manual-offset*
- *kafka-avro/producer*
- *kafka-avro/converter*
- *kafka-avro/consumer*
- *stream-app*
- *streams-app-consumer*

The additional `pom.xml` files are available in the *solutions* folder of each project.

- For creating an executable *"uber"* jar, the Maven *org.apache.maven.plugins:maven-shade-plugin* is used.
- For creating the Java classes from AVRO, the *org.apache.avro:avro-maven-plugin* is used.
   
All projects can be built and executed with

```
mvn package
java -jar target/app.jar 
```

There were three reasons for this 

- Our company uses mainly ***Maven*** as the build tool - not *gradle*.
- The gradle integration is built on some external gradle plugins, that are not from *Apache* or *Confluent Inc.* like `com.github.johnrengelman.shadow (2.0.4)` and `com.commercehub.gradle.plugin.avro (0.14.2)`.
- The gradle setup of the original *confluentic* training project, didn't work well with standard `apt install gradle` versions or  the Eclipse built-in gradle wrapper.
  
For some of the projects minor changes have to be made:

- manual-offset

  - Change the absolute folder name to `final String OFFSET_FILE_PREFIX = "./data/offset_";` and `mkdir data` in advance.
  
- kafka-avro/producer
  - Change the absolute folder name to  `private final static String INPUT_PATH_NAME = "../../../datasets/shakespeare";`
