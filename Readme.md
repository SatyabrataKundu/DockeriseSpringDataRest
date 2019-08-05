## Dockerise Spring Boot, PostgreSQL, JPA, DATA REST API



## Steps to Setup

**1. Clone the repository**

https://github.com/SatyabrataKundu/DockeriseSpringDataRest.git

**2. Configure PostgreSQL in local**

First open PGAdmin, create a database named `FnD`. Then, open `src/main/resources/application.properties` file and change the spring datasource username and password as per your PostgreSQL installation.

## Spring DATASOURCE (DataSourceAutoConfiguration & DataSourceProperties)
spring.datasource.url=jdbc:postgresql://localhost:5432/FnD
spring.datasource.username= postgres
spring.datasource.password=postgres

# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect

# Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto = update
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true 

**3. Run the app**

Type the following command from the root directory of the project to run it -

```bash
mvn spring-boot:run
```
you can package the application in the form of a JAR file and then run it like so -

```bash
mvn clean package
java -jar target/FnD-POC-JPA-DATA-REST-0.0.1-SNAPSHOT.jar
```
**3. RUN the DOCKERISE APP**

spring-boot-postgresql-jpa-hibernate-rest-api-demo-master\Dockerize>docker-compose up

Building db
Step 1/5 : FROM postgres:latest
 ---> 53912975086f
Step 2/5 : ENV POSTGRES_USER postgres
 ---> Running in 52fef8c86ea8
Removing intermediate container 52fef8c86ea8
 ---> 8c3159f2887f
Step 3/5 : ENV POSTGRES_PASSWORD postgres
 ---> Running in a58a7ac7a3ad
Removing intermediate container a58a7ac7a3ad
 ---> 32db25fe1e73
Step 4/5 : ENV POSTGRES_DB FnD
 ---> Running in 82edcb10cbae
Removing intermediate container 82edcb10cbae
 ---> e897b8f9a9ab
Step 5/5 : ADD init.sql /docker-entrypoint-initdb.d
 ---> a6f3db3b079f
Successfully built a6f3db3b079f
Successfully tagged dockerize_db:latest
WARNING: Image for service db was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Building web
Step 1/4 : FROM openjdk:8
 ---> 27da2af61908
Step 2/4 : COPY target/SpringBoot-JPA-DATA-REST-0.0.1-SNAPSHOT.jar /app.jar
 ---> 2d3efceee9a2
Step 3/4 : EXPOSE 8080/tcp
 ---> Running in d674a61a76af
Removing intermediate container d674a61a76af
 ---> 19007f38c7d4
Step 4/4 : ENTRYPOINT ["java", "-jar", "/app.jar"]
 ---> Running in c710f3119c6d
Removing intermediate container c710f3119c6d
 ---> de7a907976f3
Successfully built de7a907976f3
Successfully tagged dockerize_web:latest
WARNING: Image for service web was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating dockerize_db_1 ... done
Creating dockerize_web_1 ... done
Attaching to dockerize_db_1, dockerize_web_1
db_1   | 2019-08-02 17:31:18.484 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db_1   | 2019-08-02 17:31:18.484 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db_1   | 2019-08-02 17:31:18.739 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db_1   | 2019-08-02 17:31:19.284 UTC [22] LOG:  database system was shut down at 2019-08-02 17:08:19 UTC
db_1   | 2019-08-02 17:31:20.037 UTC [1] LOG:  database system is ready to accept connections
web_1  |
web_1  |   .   ____          _            __ _ _
web_1  |  /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
web_1  | ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
web_1  |  \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
web_1  |   '  |____| .__|_| |_|_| |_\__, | / / / /
web_1  |  =========|_|==============|___/=/_/_/_/
web_1  |  :: Spring Boot ::        (v2.0.1.RELEASE)
