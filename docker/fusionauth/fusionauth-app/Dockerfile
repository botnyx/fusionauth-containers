#
# FusionAuth App Dockerfile
#
# Build:
#   > docker build -t fusionauth/fusionauth-app:1.17.1 .
#   > docker build -t fusionauth/fusionauth-app:latest .
#
# Run:
#  > docker run -p 9011:9011 -it fusionauth/fusionauth-app
#
# Publish:
#   > docker push fusionauth/fusionauth-app:1.17.1
#   > docker push fusionauth/fusionauth-app:latest
#

FROM fusionauth/fusionauth-app:latest as fusionauth 



#FROM arm64v8/alpine:3.7 as build
#FROM fusionauth/fusionauth-java:14-jdk-alpine3.11.5
#FROM botnyx/fusionauth-java-aarch64


RUN wget https://github.com/AdoptOpenJDK/openjdk14-binaries/releases/download/jdk-14.0.1%2B7/OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  \
  && tar -zxvf OpenJDK14U-jdk_aarch64_linux_hotspot_14.0.1_7.tar.gz  --directory=/tmp












FROM arm64v8/alpine:3.7
RUN mkdir -p /opt/openjdk
COPY --from=fusionauth /tmp/jdk-14.0.1+7 /opt/openjdk



RUN addgroup fusionauth \
  && adduser -G fusionauth -D -H fusionauth

COPY --chown=fusionauth:fusionauth --from=fusionauth /usr/local/fusionauth /usr/local/fusionauth

###### Start FusionAuth App #########################################
LABEL description="Create an image running FusionAuth App. Installs FusionAuth App"
LABEL maintainer="FusionAuth <dev@fusionauth.io>"
EXPOSE 9011
USER fusionauth
ENV FUSIONAUTH_USE_GLOBAL_JAVA=1
CMD ["/usr/local/fusionauth/fusionauth-app/apache-tomcat/bin/catalina.sh", "run"]
