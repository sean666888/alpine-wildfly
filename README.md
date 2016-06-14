alpine-wildfly
==============
Docker image for running Java EE applications in [Wildfly](http://www.wildfly.org/). Based on Alpine Linux and OpenJDK. Use this image as base image for you application image.

Usage
--------

Create a Dockerfile in your project root:
~~~~
FROM njmittet/alpine-wildfly:10.0.0.Final
ADD ./target/application.war /opt/jboss/wildfly/standalone/deployments/application.war
~~~~

Build and run the application container:
~~~~
docker build -t application .
docker run -it --rm -name myapp application
~~~~

Configuration
-------------
[Start Wildfly](https://docs.jboss.org/author/display/WFLY10/Getting+Started+Guide#GettingStartedGuid0e-StartingWildFly10) with different configurations.

The default Web profile requires no configuration.

Start Wildfly with the Full profile: 
~~~~
docker run -it --rm -e STANDALONE=standalone-full -name myapp application  
~~~~

Add a custom configuration file to your Dockerfile:
~~~~
ADD ./standalone-custom.xml /opt/jboss/wildfly/standalone/configuration/standalone.xml
~~~~

Wildfly also comes with a [High Availability](https://docs.jboss.org/author/display/WFLY10/High+Availability+Guide) configuration.
~~~~
docker run -it --rm -e STANDALONE=standalone-full-ha -name myapp application  
~~~~
