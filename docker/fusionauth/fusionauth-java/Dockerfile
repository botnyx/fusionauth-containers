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

RUN apk add wget

RUN wget https://github.com/AdoptOpenJDK/openjdk14-binaries/releases/download/jdk-14.0.1%2B7/OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  \
  && tar -zxvf OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  --directory=/tmp






FROM alpine:3.11.5

COPY --from=build /tmp/jdk-14.0.1+7 /opt/openjdk








RUN ls -latr /opt/openjdk


  



ENV JAVA_HOME=/opt/openjdk/
ENV PATH=$PATH:$JAVA_HOME/bin
