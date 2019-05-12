# Java Tools Build


## **Author: Nathan Tran**


# TOOLS BUILD


## MAVEN


### Introduction



*   Maven is a build tool, a project management tool.
    *   Produces one artifact (component).
    *   Manage dependencies.
    *   Handles versioning and release.
*   Maven is open source managed by the Apache Software Foundation.
*   Base on the concept of a Project Object Model (POM)


### Environment Setup


#### System Requirement



*   Java JDK 1.7 or above


#### Install



*   Download Maven Archive: [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)
*   SDKMAN: [https://sdkman.io/sdks#maven](https://sdkman.io/sdks#maven)


### Folder Structure



*   Source code: ${basedir}/src/main/java
*   Resource code: ${basedir}/src/main/resources
*   Test: ${basedir}/src/test/java
*   Resource test: ${basedir}/src/test/resource
*   pom.xml
*   Complied byte code: ${basedir}/target 
    *   classes
    *   maven-archive
    *   surefire
    *   test-classes
    *   *.jar


### POM


```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>2.1.4.RELEASE</version>
       <relativePath/> <!-- lookup parent from repository -->
   </parent>
   <groupId>com.nathan.application</groupId>
   <artifactId>maven-spring</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <name>maven-spring</name>
   <description>Project for Spring Boot</description>

   <properties>
       <java.version>12</java.version>
   </properties>

   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-data-jpa</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-validation</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>

       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-devtools</artifactId>
           <scope>runtime</scope>
       </dependency>
       <dependency>
           <groupId>com.h2database</groupId>
           <artifactId>h2</artifactId>
           <scope>runtime</scope>
       </dependency>
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <scope>runtime</scope>
       </dependency>
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   </dependencies>

   <build>
       <plugins>
           <plugin>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-maven-plugin</artifactId>
           </plugin>
       </plugins>
   </build>

</project>
```


[Maven POM](https://www.tutorialspoint.com/maven/maven_pom.htm)



1. Project root
    *   Specify the basic schema settings such as Apache schema and w3.org specification
2. Model version
    *   Should be 4.0.0
3. Project information
    *   GroupId
        *   Id of the project's group
        *   Unique amongst an organization or a project
    *   ArtifactId
        *   Id of the project
        *   Name of the project
        *   Along with the groupId, the artifactId defines the artifact's location within the repository
    *   Version
        *   The version of the project
        *   Along with the groupId, It is used within an artifact's repository to separate versions from each other
    *   Packaging
4. Dependencies: transitive dependencies will be pulled in by Maven
    *   GroupId
    *   ArtifactId
    *   Version
    *   Scope
        *   Compile (default)
            *   Artifacts available everywhere
        *   Provided (same compile)
            *   Artifacts us going to be provided when it is deployed
        *   Run-time
            *   Not needed for compilation
            *   But needed for execution
                *   Not available for compilation, but included in all other phases
                *   Not included in the final artifact
        *   Test
            *   Only available for the test compilation and execution phase
        *   System (same provided)
            *   Specify a path to the jar on the file system
                *   Very brittle and defeats the purpose of Maven
                *   Do not use!
        *   Import
            *   Advanced topic
            *   Deals with dependencyManagement sections
5. Build
    *   Plugins
        *   Goals
        *   Phases
            *   Validate: validate the project is correct and all necessary information is available
            *   Compile: compile the source code of the project
            *   Test: test the compiled source code
            *   Package: packages the code in its defined package (jar, war, …)
            *   Integration-test: deploy and run integration test 
            *   Verify: run check against package to verify the integrity
            *   Install: install the package in the local repo
            *   Deploy: copy the final package to a remote repository
        *   Plugin Types
            *   Build plugins
                *   They execute during the build process and should be configured in the <build/> element of pom.xml.
            *   Reporting plugins
                *   They execute during the site generation process and they should be configured in the <reporting/> element of the pom.xml.
        *   Common plugins
            *   Clean
                *   Cleans up target after the build. 
                *   Deletes the target directory.
            *   Compiler
                *   Compiles Java source files.
            *   Surefire
                *   Runs the JUnit unit tests. 
                *   Creates test reports.
            *   Jar
                *   Builds a JAR file from the current project.
            *   Source
                *   
            *   Javadoc
                *   Generates Javadoc for the project.
            *   Antrun
                *   Runs a set of ant tasks from any phase mentioned of the build.
    *   Directory structure
6. Repositories
    *   A repository is a directory where all the project jars, library jar, plugins or any other project specific artifacts are stored and can be used by Maven easily.
    *   Types: 3

		![Maven Repositories](https://www.tutorialspoint.com/maven/images/repository_structure.jpg)
	
        *   Local Repo
            *   Maven local repository is a folder location on the machine
            *   Maven local repository keeps the project's all dependencies (library jars, plugin jars, etc.)
            *   When running a Maven build, then Maven automatically downloads all the dependency jars into the local repository
            *   It helps to avoid references to dependencies stored on the remote machine every time a project is built.
            *   Home/.m2
            *   User/<username>/.m2/repository
        *   Central Repo
            *   Maven central repository is a repository provided by the Maven community. 
            *   It contains a large number of commonly used libraries
            *   When Maven does not find any dependency in the local repository, it starts searching in the central repository using following URL − [https://repo1.maven.org/mavethe n2/](https://repo1.maven.org/maven2/) 
        *   Remote Repo
            *   Remote Repo is the developer's own custom repository containing required libraries or other project jars
        *   Dependency Repository
            *   When execute Maven build commands, Maven starts looking for dependency libraries in the following sequence
                *   Step 1 − Search dependency in the local repository, if not found, move to step 2 else perform further processing.
                *   Step 2 − Search dependency in the central repository, if not found and remote repository/repositories is/are mentioned then move to step 4. Else it is downloaded to the local repository for future reference.
                *   Step 3 − If a remote repository has not been mentioned, Maven simply stops the processing and throws an error (Unable to find dependency).
                *   Step 4 − Search dependency in remote repository or repositories, if found then it is downloaded to the local repository for future reference. Otherwise, Maven stops processing and throws an error (Unable to find dependency).
        *   Plugin Repository


### Build Lifecycle



*   A Build Lifecycle is a well-defined sequence of phases.
*   Which define the order in which the goals are to be executed. 
*   Here phase represents a stage in the life cycle.

<table>
  <tr>
   <td>
Phase
   </td>
   <td>Handles
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>prepare-resources
   </td>
   <td>resource copying
   </td>
   <td>Resource copying can be customized in this phase.
   </td>
  </tr>
  <tr>
   <td>validate
   </td>
   <td>Validating the information
   </td>
   <td>Validates if the project is correct and if all necessary information is available.
   </td>
  </tr>
  <tr>
   <td>compile
   </td>
   <td>compilation
   </td>
   <td>Source code compilation is done in this phase.
   </td>
  </tr>
  <tr>
   <td>Test
   </td>
   <td>Testing
   </td>
   <td>Tests the compiled source code suitable for the testing framework.
   </td>
  </tr>
  <tr>
   <td>package
   </td>
   <td>packaging
   </td>
   <td>This phase creates the JAR/WAR package as mentioned in the packaging in POM.xml.
   </td>
  </tr>
  <tr>
   <td>install
   </td>
   <td>installation
   </td>
   <td>This phase installs the package in the local maven repository.
   </td>
  </tr>
  <tr>
   <td>Deploy
   </td>
   <td>Deploying
   </td>
   <td>Copies the final package to the remote repository.
   </td>
  </tr>
</table>




*   There are always pre and post phases to register goals
*   When Maven starts building a project, it steps through a defined sequence of phases and executes goals, which are registered with each phase
*   A goal represents a specific task which contributes to the building and managing of a project
    *   It may be bound to zero or more build phases. 
    *   A goal not bound to any build phase could be executed outside of the build lifecycle by direct invocation.
*   When a phase is called via Maven command, for example, mvn compile, only phases up to and including that phase will execute.
*   Different maven goals will be bound to different phases of Maven lifecycle depending upon the type of packaging (JAR / WAR / EAR).
*   The order of execution depends on the order in which the goal(s) and the build phase(s) are invoked
    *   Clean Lifecycle
        *   **_pre-clean_**
        *   **_clean_**
        *   **_post-clean_**
    *   Default (or Build) Lifecycle: used to build the application
        *   **_Validate_**: Validates whether the project is correct and all necessary information is available to complete the build process.
        *   **_Initialize_**: Initializes build the state, for example, set properties.
        *   **_Generate-sources_**: Generate any source code to be included in the compilation phase.
        *   **_Process-sources_**: Process the source code, for example, filter any value.
        *   **_Generate-resources_**: Generate resources to be included in the package.
        *   **_Process-resources_**: Copy and process the resources into the destination directory, ready for packaging phase.
        *   **_Compile_**: Compile the source code of the project.
        *   **_Process-classes_**: Post-process the generated files from the compilation, for example, to do bytecode enhancement/optimization on Java classes.
        *   **_Generate-test-sources_**: Generate any test source code to be included in the compilation phase.
        *   **_Process-test-sources_**: Process the test source code, for example, filter any values.
        *   **_Test-compile_**: Compile the test source code into the test destination directory.
        *   **_Process-test-classes_**: Process the generated files from test code file compilation.
        *   **_Test_**: Run tests using a suitable unit testing framework (JUnit is one).
        *   **_Prepare-package_**: Perform any operations necessary to prepare a package before the actual packaging.
        *   **_Package_**: Take the compiled code and package it in its distributable formats, such as a JAR, WAR, or EAR file.
        *   **_Pre-integration-test_**: Perform actions required before integration tests are executed. For example, setting up the required environment.
        *   **_Integration-test_**: Process and deploy the package if necessary into an environment where integration tests can be run.
        *   **_Post-integration-test_**: Perform actions required after integration tests have been executed. For example, cleaning up the environment.
        *   **_Verify_**: Run any check-ups to verify the package is valid and meets quality criteria.
        *   **_Install_**: Install the package into the local repository, which can be used as a dependency in other projects locally.
        *   **_Deploy_**: Copies the final package to the remote repository for sharing with other developers and projects.
    *   Site Lifecycle: Maven Site plugin is generally used to create fresh documentation to create reports, deploy the site, etc
        *   pre-site
        *   site
        *   post-site
        *   site-deploy


### Build Profile



*   A Build profile is a set of configuration values, which can be used to set or override default values of Maven build
*   Can customize build for different environments such as Production v/s Development environments.
*   Profiles are specified in the pom.xml file using its activeProfiles/profiles elements and are triggered in a variety of ways.
*   Profiles modify the POM at build time and are used to give parameters different target environments (for example, the path of the database server in the development, testing, and production environments).
*   Profile Activation
    *   Explicitly using command console input.
    *   Through maven settings.
    *   Based on environment variables (User/System variables).
    *   OS Settings (for example, Windows family).
    *   Present/missing files.


### Snapshots



*   SNAPSHOT is a special version that indicates a current development copy. 
*   Unlike regular versions, Maven checks for a new SNAPSHOT version in a remote repository for every build.
*   Snapshot vs Version
    *   In case of Version, if Maven once downloaded the mentioned version, say data-service:1.0, it will never try to download a newer 1.0 available in the repository. To download the updated code, the data-service version is being upgraded to 1.1.
    *   In the case of SNAPSHOT, Maven will automatically fetch the latest SNAPSHOT (data-service:1.0-SNAPSHOT) every time app-ui team build their project.


### CLI - Goals



1. Clean
    *   Deletes the target directory and any generated resource.
2. Compile
    *   Compiles all source code,
    *   Generates any file,
    *   Copies resource to the classes directory
3. Package
    *   Runs the compile command first,
    *   Runs any tests,
    *   Packages the app based off of its packaging type
4. Install (Local Repo)
    *   Runs the package command and then
    *   Installs it in the local repo
5. Deploy (Remote Repo)
    *   Runs the install command and then
    *   Deploys it to a corporate repo


## GRADLE


## BAZEL


# LINKS REFERENCE



*   [Maven Tutorial](https://www.tutorialspoint.com/maven/index.htm)

<!-- Docs to Markdown version 1.0β17 -->

