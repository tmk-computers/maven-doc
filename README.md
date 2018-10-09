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

# pom.xml Can be divided into 4 basic parts:
- Project Information
    - groupId
    - artifactId
    - version
    - packaging
- Dependencies
    - Direct dependencies used in our application
- Build
    - Plugins
    - Directory Structure
- Repositories
    - Where we download the artifacts from
    
# Build Lifecycle
- Maven is based around the central concept of a build lifecycle. What this means is that the process for building and distributing a particular artifact (project) is clearly defined.

- For the person building a project, this means that it is only necessary to learn a small set of commands to build any Maven project, and the POM will ensure they get the results they desired.

- There are three built-in build lifecycles: default, clean and site. The default lifecycle handles your project deployment, the clean lifecycle handles project cleaning, while the site lifecycle handles the creation of your project's site documentation.
A Build Lifecycle is Made Up of Phases

- Each of these build lifecycles is defined by a different list of build phases, wherein a build phase represents a stage in the lifecycle.

- For example, the default lifecycle comprises of the following phases (for a complete list of the lifecycle phases, refer to the Lifecycle Reference):

    - **validate** - validate the project is correct and all necessary information is available
    - **compile** - compile the source code of the project
    - **test** - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
    - **package** - take the compiled code and package it in its distributable format, such as a JAR.
    - **verify** - run any checks on results of integration tests to ensure quality criteria are met
    - **install** - install the package into the local repository, for use as a dependency in other projects locally
    - **deploy** - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.
    
# Usual Command Line Calls

- In a development environment, use the following call to build and install artifacts into the local repository.

    - mvn install

- This command executes each default life cycle phase in order (validate, compile, package, etc.), before executing install. You only need to call the last build phase to be executed, in this case, install:

- In a build environment, use the following call to cleanly build and deploy artifacts into the shared repository.

    - mvn clean deploy

- The same command can be used in a multi-module scenario (i.e. a project with one or more subprojects). Maven traverses into every subproject and executes clean, then executes deploy (including all of the prior build phase steps).

## Dependency Scope

- Dependency scope is used to limit the transitivity of a dependency, and also to affect the classpath used for various build tasks.

- There are 6 scopes available:

    - **compile** - This is the default scope, used if none is specified. Compile dependencies are available in all classpaths of a project. Furthermore, those dependencies are propagated to dependent projects.
    
            <dependencies>
                <dependency>
                    <groupId>log4j</groupId>
                    <artifactId>log4j</artifactId>
                    <version>1.2.14</version>
                    <!-- You can ommit this because it is default -->
                    <scope>compile</scope>
                </dependency>
            </dependencies>
        
    - **provided** - This is much like compile, but indicates you expect the JDK or a container to provide the dependency at runtime. For example, when building a web application for the Java Enterprise Edition, you would set the dependency on the Servlet API and related Java EE APIs to scope provided because the web container provides those classes. This scope is only available on the compilation and test classpath, and is not transitive.
    
            <dependency>
                <groupId>javax.servlet</groupId>
                <artifactId>servlet-api</artifactId>
                <version>3.0.1</version>
                <scope>provided</scope>
            </dependency>
    
    - **runtime** - This scope indicates that the dependency is not required for compilation, but is for execution. It is in the runtime and test classpaths, but not the compile classpath.
    
    
            <dependency>
                <groupId>com.thoughtworks.xstream</groupId>
                <artifactId>xstream</artifactId>
                <version>1.4.4</version>
                <scope>runtime</scope>
            </dependency>
    
    
    - **test** - This scope indicates that the dependency is not required for normal use of the application, and is only available for the test compilation and execution phases. This scope is not transitive.
    
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.12</version>
                <scope>test</scope>
            </dependency>
    
    - **system** - This scope is similar to provided except that you have to provide the JAR which contains it explicitly. The artifact is always available and is not looked up in a repository.
    
            <dependency>
                <groupId>extDependency</groupId>
                <artifactId>extDependency</artifactId>
                <scope>system</scope>
                <version>1.0</version>
                <systemPath>${basedir}\war\WEB-INF\lib\extDependency.jar</systemPath>
            </dependency>
    
    - **import** - This scope is only supported on a dependency of type pom in the <dependencyManagement> section. It indicates the dependency to be replaced with the effective list of dependencies in the specified POM's <dependencyManagement> section. Since they are replaced, dependencies with a scope of import do not actually participate in limiting the transitivity of a dependency.
    
            <dependencyManagement>
                <dependencies>
                    <dependency>
                        <groupId>other.pom.group.id</groupId>
                        <artifactId>other-pom-artifact-id</artifactId>
                        <version>SNAPSHOT</version>
                        <scope>import</scope>
                        <type>pom</type>
                    </dependency>  
                </dependencies>
            </dependencyManagement>
    

## Maven multi-module project
    .
    ├── modules-root
    │   ├── moduleA
    │   │   └── pom.xml <--- Module A POM
    │   ├── moduleB
    │   │   └── pom.xml <--- Module B POM
    │   └── pom.xml     <--- modules root
    └── pom.xml         <--- project-root
    
- Let's start with the project-root, which will look like this:

        <groupId>org.test</groupId>
        <artifactId>project-root</artifactId>
        <packaging>pom</packaging>
        <version>1.0.0-SNAPSHOT</version>

        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>junit</groupId>
                    <artifactId>junit</artifactId>
                    <version>4.11</version>
                    <scope>test</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>

        <modules>
            <module>modules-root</module>
        </modules>
            
- The module parent will look like this. I will emphasis that this contains only the reference to the moduleA and moduleB and will inherit from the project-root:

        <parent>
            <groupId>org.test</groupId>
            <artifactId>super-pom</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </parent>

        <groupId>org.test.module</groupId>
        <artifactId>modules-root</artifactId>
        <packaging>pom</packaging>

        <modules>
            <module>moduleA</module>
            <module>moduleB</module>
        </modules>
    
- moduleA will look like this. Pay attention that this will inherit from module-parent (parent) which is exactly one level above...

        <parent>
            <groupId>org.test.module</groupId>
            <artifactId>module-parent</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </parent>

        <artifactId>moduleA</artifactId>
        <packaging>..</packaging>

        <....other dependencies..>
## Repositories     
### Local Repo
- Where Maven stores everything it downloads
    - Installs in your **"home directory"\.m2**
    - C:\Users\<yourusername>\.m2\repository
    
        <dependency>
            <groupId>commons-lang</groupId>
            <artifactId>commons-lang</artifactId>
            <version>2.1</version>
        </dependency>
    
- Stores artifacts using the information that you provided for **artifactId**, **groupId**, and **version**
    - C:\Users\<yourusername>\.m2\repository\commons-lang\commons-lang\2.1\commons-lang-2.1.jar
- Avoids duplication by copying it in every project and storing it in your SCM



## Versions
- **Development starts off as a SNAPSHOT**
    - myapp-1.0-SNAPSHOT.jar
    - Changes always downloaded
    - Saves you from rereleasing versions for development
    - Never deploy to production with a SNAPSHOT
- **A release doesn’t have a specific naming convention**
    - myapp-1.0.jar
    - myapp-1.0.1.jar
- **Industry common terms, but don’t affect maven**
    - myapp-1.0-M1.jar (milestone release)
    - myapp-1.0-RC1.jar (release candidate)
    - myapp-1.0-RELEASE.jar (release)
    - myapp-1.0-Final.jar (release)
    
## core packaging types:
- pom, jar, maven-plugin, ejb, war, ear, rar, par
- The default packaging type is jar
- The type of pom is referred to as a dependency pom
- Downloads dependencies from that pom

## Plugins

- Maven is - at its heart - a plugin execution framework; all work is done by plugins. Looking for a specific goal to execute? This page lists the core plugins and others. There are the build and the reporting plugins:

    - **Build plugins** will be executed during the build and they should be configured in the **<build/>** element from the POM.
    - **Reporting plugins** will be executed during the site generation and they should be configured in the **<reporting/>** element from the POM. Because the result of a Reporting plugin is part of the generated site, Reporting plugins should be both internationalized and localized. 

