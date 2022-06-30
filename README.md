# Project Creation and POM File

## Learning Goals

- Create an empty Maven project.
- Create and understand the basic directory structure.

## Introduction

A directory that has a `pom.xml` file is a valid Maven project. A POM (Project
Object Model) file describes what libraries are needed for your projects, which
Java version to build, plugins needed by Maven, and more. Let’s create our first
pom file and add some basic configuration.

## Create a Pom File

First, we will create a directory called `example-app`. This will be our
project’s root directory. Once you’ve created this folder, create a `pom.xml`
file in the `example-app` directory and add the following to the POM file:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>example-app</artifactId>
  <version>1.0-SNAPSHOT</version>

  <name>example-app</name>
  <url>http://www.example.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
  </properties>

  <dependencies>

  </dependencies>

  <build>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.10.1</version>
      </plugin>
    </plugins>
  </build>
</project>
```

We’ll start examining the pom file from the line where
`<groupId>org.example</groupId>` starts. Everything before that contains the XML
namespaces and the XML model version which you won’t have to modify. We’ll look
at the sections below that and discuss them.

### Coordinates

Since all projects need to be unique Maven provides a standard way to
distinguish between projects using
[coordinates](https://maven.apache.org/pom.html#maven-coordinates).

```xml
<groupId>org.example</groupId>
<artifactId>example-app</artifactId>
<version>1.0-SNAPSHOT</version>
```

1. **groupId:** This is usually the group, company, or department creating the
   project. We generally use the domain name in reverse order. In this case, the
   company domain is `[example.org](http://example.org)` so we’ve written it as
   `org.example` in the POM file.
2. **artifactId:** A unique name for the project under the groupId. For example,
   if the company is creating multiple libraries, each library would have a
   unique artifactId but the same groupId.
3. **version:** This indicates the current version of the project. Each new
   release would get a new version. You can check out what a SNAPSHOT version
   means
   [here](https://maven.apache.org/guides/getting-started/index.html#what-is-a-snapshot-version).

![Maven coordinates](https://curriculum-content.s3.amazonaws.com/java-mod-5/maven-coordinates.png)

In this diagram, the first layer represents the groupId, the second layer
represents artifactId, and finally the final layer represents the version.

### Project Name and URL

The `<name>` tag is a human-friendly name for the project. If it’s not
specified, the `artifactId` will be used as the project name. The `<url>` tag
links to the project so other tools can parse the project’s link.

```xml
<name>example-app</name>
<url>http://www.example.org</url>
```

### Properties

The properties section specifies values that can be used anywhere within a POM
or as default values by plugins.

```xml
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <maven.compiler.source>11</maven.compiler.source>
  <maven.compiler.target>11</maven.compiler.target>
</properties>
```

The `<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>`
specifies the encoding for resources like .properties and text files. Maven will
use the operating system’s default encoding if it’s not specified which could
lead to incompatibility across systems.

The `<maven.compiler.source>11</maven.compiler.source>` tag specifies the
minimum Java version required for the project and the
`<maven.compiler.target>11</maven.compiler.target>` tag specifies what version
the project is expected to run on.

### Dependencies

This section is used for defining additional libraries required for the project.
We will add dependencies later and discuss them in detail in later lessons.

```xml
<dependencies>

</dependencies>
```

### Build and Plugins

The `<build>` tag is used for specifying the project directory structure and
managing plugins.

Plugins are used by Maven to extend its core functionality. Some of the common
plugins are:

- Compiler Plugin: this contains the logic for compiling the project.
- Jar Plugin: contains instructions for creating JAR files.
- Surefire Plugin: used for executing unit tests.

```xml
<build>
  <plugins>
    <plugin>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.10.1</version>
    </plugin>
  </plugins>
</build>
```

There are several other plugins that we can use and even build our own. A plugin
simply consists of code that performs various tasks during the build process.
We’ve only added the `maven-compiler-plugin` to this project which is used to
compile Java sources.

## Validation

We can use the `mvn validate` command to validate the `pom.xml` file. Here’s the
output of running the command on a project with a valid file:

```bash
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.example:example-app >-----------------------
[INFO] Building example-app 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.034 s
[INFO] Finished at: 2022-06-28T21:08:06-04:00
[INFO] ------------------------------------------------------------------------
```

## Conclusion

We’ve learned how to create a Maven project and learned the basic properties of
the POM file.
