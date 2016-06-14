alpine-wildfly
==============
Docker image for running Java EE applications in [Wildfly](http://www.wildfly.org/). Based on Alpine Linux and OpenJDK.

Usage
--------
To run your application in the Docker image, either extend the Docker image or link your application into the Docker container.

Create a Dockerfile in your Java EE project directory: 
~~~~
FROM njmittet/alpine-wildfly:latest
ADD ./target/myproject.war /opt/jboss/wildfly/standalone/deployments/myproject.war
~~~~

Link the WAR-file: 
~~~~
docker run -d njmittet/alpine-wildfly:latest -v ./target/myproject.war:/opt/jboss/wildfly/standalone/deployments/myproject.war
~~~~

Configuration
-------------
[Start Wildfly](https://docs.jboss.org/author/display/WFLY10/Getting+Started+Guide#GettingStartedGuid0e-StartingWildFly10) with the Web profile (default), the Full profile, or a custom profile. 

While the Web profile is the default configuration, do the following to use the Full, or a custom profile:

Full profile:
~~~~
docker run -d njmittet/alpine-wildfly:latest -e STANDALONE=standalone-full  -v ./target/myproject.war:/opt/jboss/wildfly/standalone/deployments/myproject.war
~~~~

Custom configuration:
~~~~
docker run -d njmittet/alpine-wildfly:latest -v ./standalone-custom.xml::/opt/jboss/wildfly/standalone/configuration/standalone.xml  -v ./target/myproject.war:/opt/jboss/wildfly/standalone/deployments/myproject.war
~~~~

If linking files is not prefered, see the [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) for how to add the configuration files to your own Docker image.
Wildfly also comes with a [High Availability](https://docs.jboss.org/author/display/WFLY10/High+Availability+Guide) configuration.
