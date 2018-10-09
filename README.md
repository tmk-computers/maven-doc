# Apache Maven documentation 

## What is Apache Maven
Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information. 

#### At its simplest, Maven is a build tool
    - It always produces one artifact (component)
    - It helps us manage dependencies
#### It can also be used as a project management tool
    - It handles versioning and releases
    - Describes what your project is doing or what it produces
    - Can easily produce Javadocs as well as other site information
    
#### Why do you want to use it
    - Repeatable builds
    - We can recreate our build for any environment
#### Transitive dependencies
    - Downloading a dependency with also pull other items it needs
#### Contains everything it needs for your environment
#### Works with a local repo
#### Works with your IDE, but also standalone
#### The preferred choice for working with build tools like Jenkins or Cruise Control

## Installation
- Install JDK for your operating system
- download binary tar.gz or zip archive from https://maven.apache.org/download.cgi and extract it to convenient location
- set **JAVA_HOME** environment variable which points to your JDK installation
- set **MAVEN_HOME** environment variable which points to your Maven binary directory
- append *JDK bin directory path* and *maven bin directory path* to **PATH** environment variable
- check JDK installed and configured correctly
    - javac -version
- check java installed and configured correctly
    - mvn -v

## Creating a Project using Maven command
- mvn archetype:generate  
-DgroupId=com.mycompany.app  
-DartifactId=my-app  
-DarchetypeArtifactId=maven-archetype-quickstart  
-DinteractiveMode=false  

- Above command will create new project **my-app**
- Change into that directory.
    - cd my-app

Under this directory you will notice the following standard project structure.

    my-app
    |-- pom.xml
    `-- src
        |-- main
        |   `-- java
        |       `-- com
        |           `-- mycompany
        |               `-- app
        |                   `-- App.java
        `-- test
            `-- java
                `-- com
                    `-- mycompany
                        `-- app
                            `-- AppTest.java

The **src/main/java** directory contains the **project source code**, the **src/test/java** directory contains the **test source**, and the **pom.xml** file is the **project's Project Object Model**, or POM.
The POM

The pom.xml file is the core of a project's configuration in Maven. It is a single configuration file that contains the majority of information required to build a project in just the way you want. The POM is huge and can be daunting in its complexity, but it is not necessary to understand all of the intricacies just yet to use it effectively. This project's POM is:

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
     
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-app</artifactId>
      <version>1.0-SNAPSHOT</version>
      <!-- packaging>jar</packaging -->
     
      <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
      </properties>
     
      <dependencies>
        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.12</version>
          <scope>test</scope>
        </dependency>
      </dependencies>
    </project>

