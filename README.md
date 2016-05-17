Spring MVC 4 Quickstart Maven Archetype
=========================================

Summary
-------
The project is a Maven archetype for Spring MVC 4 web application.

Generated project characteristics
-------------------------
* No-xml Spring MVC 4 web application
* Thymeleaf, Bootstrap
* JPA (Hibernate/HSQLDB/Spring Data JPA)
* JUnit/Mockito
* Spring Security
* MongoDB (Spring Data Mongo)

Prerequisites
-------------

- JDK 8
- Maven 3

Create a project
----------------

```bash
    mvn archetype:generate \
        -DarchetypeGroupId=pl.codeleak \
        -DarchetypeArtifactId=spring-mvc-quickstart \
        -DarchetypeVersion=1.0.0 \
        -DgroupId=my.groupid \
        -DartifactId=my-artifactId \
        -Dversion=version \
        -DarchetypeRepository=http://kolorobot.github.io/spring-mvc-quickstart-archetype
```

Note: The above command will bootstrap a project using the archetype published here: http://kolorobot.github.io/spring-mvc-quickstart-archetype

Run the project
----------------

Navigate to newly created project directory (`my-artifactId`) and then run:

```bash
	mvn test tomcat7:run
```

Test in the browser
-------------------

	http://localhost:8080/

Note: No additional services are required in order to start the application. Mongo DB configuration is in place but it is not used in the code.

Install archetype locally
-------------------------

To install the archetype in your local repository execute the following commands:

```bash
    git clone https://github.com/kolorobot/spring-mvc-quickstart-archetype.git
    cd spring-mvc-quickstart-archetype
    mvn clean install
```

Create a project from a local repository
----------------------------------------

Create a new empty directory for your project and navigate into it and then run:

```bash
    mvn archetype:generate \
        -DarchetypeGroupId=pl.codeleak \
        -DarchetypeArtifactId=spring-mvc-quickstart \
        -DarchetypeVersion=1.0.0 \
        -DgroupId=my.groupid \
        -DartifactId=my-artifactId \
        -Dversion=version
```

Note: The above command will bootstrap a project using the archetype published in your local repository.

Creating a new project in Eclipse
----------------------------------

* Import archetype URI by `Import ... > Projects from Git > Clone URI`
* Install the archetype in local repository with `mvn install`
* Go to `Preferences > Maven > Archetypes` and `Add Local Catalog`
* Select the catalog from file (`archetype-catalog.xml`) 
* Create new Maven project and select the archetype (remember so select `Include snapshot archetypes`)

If you have any troubles with installation in Eclipse, you may want to have a look at this issue: #74

Creating a new project in IntelliJ
----------------------------------

* Create new project `File > New > Project`
* Click Maven on the left hand side of the new project dialog
* Check `Create from archetype`
* Click the `Add Archetype` button
* Set Group Id to `com.github.spring-mvc-archetypes`
* Set Artifact Id to `spring-mvc-quickstart`
* Set Version to `1.0.0`
* Click next and create the project

Switching to PostgreSQL
-----------------------

* Add dependency to PostgreSQL driver in POM:

```
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>9.4.1207</version>
</dependency>
```

* Change `persistence.properties`:

```
dataSource.driverClassName=org.postgresql.Driver
dataSource.url=jdbc:postgresql:postgres
dataSource.username=postgres
dataSource.password=postgres

hibernate.dialect=org.hibernate.dialect.PostgreSQL9Dialect
hibernate.hbm2ddl.auto=create
```

Enabling MongoDB repositories
-----------------------------

* Open MongoConfig class and uncomment the following line:

```
// @EnableMongoRepositories(basePackageClasses = Application.class)
```

Now you can add repositories to your project:

```
@Repository
public interface MyRepository extends MongoRepository<MyDocument, String> {

}
```
