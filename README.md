# Swagger Jakarta Maven Plugin

This plugin is intended to use the [Swagger Core library](https://github.com/swagger-api/swagger-core) to generate OpenAPI documentation from JAX-RS 3+ based REST services with as little change as possible.

This allows for @SwaggerDefinition, @ReaderListener and ModelConverters to work the same way as with the core Swagger library.

This version supports, and only supports, JAX-RS 3+ / Jakarta EE9+, i.e. after the jakarta namespace change.

# Status

The plugin is considered production ready. The version 3.x.x of the plugin is supporting generation of OpenAPI version 3 specifications using Swagger 2.x and JAX-RS 3.x.

<!--
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.openapitools.swagger/swagger-maven-plugin/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.openapitools.swagger/swagger-maven-plugin/)
[![Javadoc](https://javadoc.io/badge/io.openapitools.swagger/swagger-maven-plugin/badge.svg)](https://www.javadoc.io/doc/io.openapitools.swagger/swagger-maven-plugin)
[![Build status](https://travis-ci.org/openapi-tools/swagger-maven-plugin.svg?branch=master)](https://travis-ci.org/openapi-tools/swagger-maven-plugin)
[![Known Vulnerabilities](https://snyk.io/test/github/openapi-tools/swagger-jakarta-maven-plugin/badge.svg)](https://snyk.io/test/github/openapi-tools/swagger-jakarta-maven-plugin) 
-->

# Installation

Clone this repository.
```
git clone https://github.com/saturnbee/swagger-jakarta-maven-plugin.git
```

Install the maven plugin locally.

```
mvn install
```

# Usage

To have Swagger generate the OpenAPI specifications as part of the build add in the plugin to the POM.

```xml
<build>
  <plugins>
    ...
    <plugin>
      <groupId>io.github.saturnbee</groupId>
      <artifactId>swagger-jakarta-maven-plugin</artifactId>
      <configuration>
        <resourcePackages>
          <resourcePackage>io.openapitools.swagger.example</resourcePackage>
          <resourcePackage>io.openapitools.swagger.example.alternate</resourcePackage>
        </resourcePackages>
        <outputDirectory>${basedir}/target/</outputDirectory>
        <outputFilename>swagger</outputFilename>
        <outputFormats>JSON,YAML</outputFormats>
        <prettyPrint>true</prettyPrint>
      </configuration>
      <executions>
        <execution>
          <goals>
            <goal>generate</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
    ...
  </plugins>
</build>
```

This will run the generation in the prepare-package lifecycle stage of the Maven build.

## Specifying Packages with JAX-RS Endpoints

The packages containing JAX-RS endpoints must be configured using the resourcePackages element. See the minimal configuration above.

## Properties of Swagger model

Most general properties of the Swagger model is configurable using the swaggerConfig element. Note this may also be configured through the @OpenAPIDefinition annotation - see [Customizing your auto-generated Swagger Definitions](http://swagger.io/customizing-your-auto-generated-swagger-definitions-in-1-5-x/).

```xml
<plugin>
  <groupId>io.github.saturnbee</groupId>
  <artifactId>swagger-jakarta-maven-plugin</artifactId>
  <configuration>
    <swaggerConfig>
      <servers>
        <server>
          <url>https://services.exmple.it/base/path</url>
          <description>Endpoint URL</description>
        </server>
      </servers>
      <info>
        <title>Title</title>
        <version>1.0.0</version>
        <termsOfService>Terms</termsOfService>
        <contact>
          <email>e@mail.com</email>
          <name>My Name</name>
          <url>https://google.com</url>
        </contact>
        <license>
          <url>https://license</url>
          <name>MIT</name>
        </license>
        <extensions>
          <x-custom-field-1>my-custom-field-1</x-custom-field-1>
          <x-custom-field-2>my-custom-field-2</x-custom-field-2>
        </extensions>
      </info>
      <descriptionFile>src/test/resources/descriptions.md</descriptionFile>
    </swaggerConfig>
```


## Deploying

The generated OpenAPI specifications may be installed and deployed as Maven artifact. To enable this add the configuration parameter attachSwaggerArtifact.

```xml
<plugin>
  <groupId>io.github.saturnbee</groupId>
  <artifactId>swagger-jakarta-maven-plugin</artifactId>
  <configuration>
    <attachSwaggerArtifact>true</attachSwaggerArtifact>
```

# Acknowledgement

Thanks to the OG, [Yukai Kong](https://github.com/kongchen) for his work on [Swagger Maven plugin](https://github.com/kongchen/swagger-maven-plugin).

Thanks to [OpenAPI Tools](https://github.com/openapi-tools/), and specifically to Thor Anker Kvisgård Lange, for [Swagger Maven plugin](https://github.com/openapi-tools/swagger-maven-plugin).

Thanks to [David Gautier](https://github.com/dgautier/) for [Swagger Maven plugin](https://github.com/dgautier/swagger-maven-plugin).

