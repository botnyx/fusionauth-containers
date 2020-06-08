#
# FusionAuth Java Dockerfile
#
# Build:
#   > docker build -t fusionauth/fusionauth-java:14-jdk-alpine3.11.5 .
#
# Publish:
#   > docker push fusionauth/fusionauth-java:14-jdk-alpine3.11.5
#   > docker push fusionauth/fusionauth-java:latest
#

FROM openjdk:14-jdk-alpine3.10 as build

RUN /opt/openjdk-14/bin/jlink --compress=2 \
     --module-path /opt/openjdk-14/jmods/ \
     --add-modules java.base,java.compiler,java.desktop,java.instrument,java.management,java.naming,java.rmi,java.security.jgss,java.security.sasl,java.sql,java.xml.crypto,jdk.attach,jdk.crypto.ec,jdk.jdi,jdk.localedata,jdk.scripting.nashorn,jdk.unsupported \
     --output /jlinked

FROM alpine:3.11.5
COPY --from=build /jlinked /opt/openjdk

RUN apk add curl

RUN curl -Sk --progress-bar https://github.com/AdoptOpenJDK/openjdk14-binaries/releases/download/jdk-14.0.1%2B7/OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz -o openjdk.tar.gz \
  && tar -zxvf openjdk.tar.gz /opt/openjdk
  



ENV JAVA_HOME=/opt/openjdk/
ENV PATH=$PATH:$JAVA_HOME/bin
