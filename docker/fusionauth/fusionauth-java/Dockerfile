#FROM arm64v8/alpine:3.7
#RUN curl -SkL --progress-bar https://github.com/AdoptOpenJDK/openjdk14-binaries/releases/download/jdk-14.0.1%2B7/OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz -o OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz \
#  && tar -zxvf OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  --directory=/tmp
#COPY --from=build /tmp/jdk-14.0.1+7 /opt/openjdk
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

# the image below us not available for arm64
#FROM openjdk:14-jdk-alpine3.10 as build
# we use a generic build.
FROM alpine:latest as build

# add curl for downloading openjdk
RUN apk add curl

#RUN /opt/openjdk-14/bin/jlink --compress=2 \
#     --module-path /opt/openjdk-14/jmods/ \
#     --add-modules java.base,java.compiler,java.desktop,java.instrument,java.management,java.naming,java.rmi,java.security.jgss,java.security.sasl,java.sql,java.xml.crypto,jdk.attach,jdk.crypto.ec,jdk.jdi,jdk.localedata,jdk.scripting.nashorn,jdk.unsupported \
#     --output /jlinked

# download and unpack openjdk v14
RUN curl -SkL --progress-bar https://github.com/AdoptOpenJDK/openjdk14-binaries/releases/download/jdk-14.0.1%2B7/OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz -o OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz \
  && tar -zxvf OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  --directory=/tmp


RUN mv /tmp/jdk-14.0.1+7 /jlinked



FROM alpine:3.11.5
COPY --from=build /jlinked /opt/openjdk

ENV JAVA_HOME=/opt/openjdk/
ENV PATH=$PATH:$JAVA_HOME/bin
