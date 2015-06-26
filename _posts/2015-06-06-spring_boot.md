---
layout: post
title: Microservices with Spring Boot
---

Microservices with Spring Boot
=========================

Nowadays microservices is becoming a popular architecture style. One of famous way that use to implement microservices is create service as a RESTFul API.

There are many frameworks that let us to create a RESTFul API easily by provide set of method and/or library that you can call for accomplishing a basic RESTFul API function like handle http request, json serialisation, json deserialisation, etc.

One of famous microservices framework is spring boot with spring boot you just create a few class (or just one class) and build it into single jar file, spring boot will embed tomcat(as default) into your jar, you just run that jar with simple *java -jar* command and then you will have RESTFul API up and running. Spring boot support dependencies injection out of the box.

### Spring Boot Demo ###
Now we will create demo application with spring boot. This application is a simple CRUD RESTFul API on blog data.

**pom.xml**

This is pom.xml of our project.
[[d1abbcd9dddf3e0e91364cc4ce81017b]]
let explore our pom.xml a bit, our pom used spring's spring-boot-starter-parent as a parent pom, as parent deceleration below.

         <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>1.2.1.RELEASE</version>
         </parent>

This allow out project just declare only one dependencies

         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

actually our project just inherit set of dependencies from spring-boot's parent. This is enough to make our project up and running.

We also use plugin call spring-boot-maven-plugin this plugin will help use when we need to run and package our application (you will see letter)

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>1.2.2.RELEASE</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

**domain class**

We are building blog api so we need Blog class as a domain class.
[[61adb8c4ac04a53caec29aad1eb3040e]]

**repository**

Repository class will responsible for data access but in our demo we don't want to involve with database setup, create table script,  database driver etc., so we just create repository with Map inside to simulate database table. Our repository has method for CRUD operation and annotated with spring's *@Repository* this let we can use annotation like *@Autowired* when we want to use this class.
[[ae605083e3832f72f998b4bcbdf22e85]]

**controller**

Controller class is responsible for handle HTTP request that send from client and create HTTP response and send it back to client. Our controller annotate with *@RestController* and has mapping with GET for client to get blog's information, POST for client to create new blog and DELETE for client to delete blog. This controller we use *@Autowired* to let spring handle dependencies for us which is BlogRepository in this case.
[[88f99ff63cc428a10fb990a5dc606ea7]]

**main class**

As said before our service will run with *java -jar* command no need any servlet container. All it need just main class where our application start from.
[[3ca3626a180e85b5707c9f594a4386d0]]
our Application class annotate with *@EnableAutoConfiguration*  this annotation tells Spring Boot to “guess” how you will want to configure Spring, based on the jar dependencies that you have added. Since spring-boot-starter-web added Tomcat and Spring MVC, the auto-configuration will assume that you are developing a web application and setup Spring accordingly and we also have *@ComponentScan* to enable spring's component scan on our project.

**build and run**

Now time to see the result.

Use this command to pack our application into jar file.

        mvn package
after build you will find our application package *springbootblog-1.0-SNAPSHOT.jar*	 in target directory.

Use this command to run our application.

        java -jar target/springbootblog-1.0-SNAPSHOT.jar
Now you will have service up and running at

        http://localhost:8080/
some of you might already open this url with web browser and found some kind of error page because this is not how our service suppose to use.

**test our RESTFul API**

Working with RESTFul API you need rest client to interact with RESTFul API I suggest [postman](http://www.getpostman.com)

get all blog : to get all blog from service you can use rest client to make request with GET method to this url

        http://localhost:8080/blogs
you will got response like this

	[
		{
			"id": 1,
			"title": "Java is cool",
			"author": "tum",
			"text": "How java cool"
		},
		{
			"id": 2,
			"title": "Spring is cool",
			"author": "tum",
			"text": "What is spring framework"
		}
	]
this this all blog entry in our system(initial data) response as a json format.

get blog with specific id : if you want to get just only one blog entry with specific id you can use rest client to make request with GET method to this url

    http://localhost:8080/blogs/1
this will return blog entry that has id 1.

    {
        "id": 1,
        "title": "Java is cool",
        "author": "tum",
        "text": "How java cool"
    }
create new blog entry : with RESTFul API you can create new entry by use POST method with request body like this

    {
        "id": null,
        "title": "Java is dead",
        "author": "steve",
        "text": "Nobody use java anymore"
    }
after send request list all blog again you should see your new entry.

delete blog entry : with RESTFul API you can create new entry by use DELETE method and specify entry that you want to delete for example if we want to delete blog entry with id 1, just use DELETE method to this url

    http://localhost:8080/blogs/1
list all blog again blog entry with id 1 should be gone.

### Source code ###

You will found all source code of this project here :
[source code](https://github.com/tsongpon/springbootblog)
