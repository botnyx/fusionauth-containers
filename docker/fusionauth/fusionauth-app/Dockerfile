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

FROM arm64v8/alpine:3.7



RUN addgroup fusionauth && adduser -G fusionauth -D -H fusionauth

COPY --chown=fusionauth:fusionauth --from=fusionauth/fusionauth-app:latest /usr/local/fusionauth /usr/local/fusionauth

COPY --from=botnyx/fusionauth-java-aarch64 /opt/openjdk /opt/openjdk

###### Start FusionAuth App #########################################
LABEL description="Create an image running FusionAuth App. Installs FusionAuth App"
LABEL maintainer="FusionAuth <dev@fusionauth.io>"
EXPOSE 9011
USER fusionauth
ENV FUSIONAUTH_USE_GLOBAL_JAVA=1
CMD ["/usr/local/fusionauth/fusionauth-app/apache-tomcat/bin/catalina.sh", "run"]

