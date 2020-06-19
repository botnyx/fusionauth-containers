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

FROM adoptopenjdk:14-jdk-hotspot-bionic as build

###### Install stuff we need and then cleanup cache #################
RUN apt update && apt install unzip

###### Get and install FusionAuth App Bundle ########################
#ENV FUSIONAUTH_VERSION=1.17.1
RUN curl -Sk --progress-bar https://storage.googleapis.com/inversoft_products_j098230498/products/fusionauth/${FUSIONAUTH_VERSION}/fusionauth-app-${FUSIONAUTH_VERSION}.zip -o fusionauth-app.zip \
  && mkdir -p /usr/local/fusionauth/fusionauth-app \
  && unzip -nq fusionauth-app.zip -d /usr/local/fusionauth


FROM adoptopenjdk:14-jdk-hotspot-bionic


#RUN addgroup fusionauth && adduser -G fusionauth -D -H fusionauth
RUN groupadd fusionauth
RUN useradd -r -s /bin/sh -g fusionauth -u 1001 fusionauth


# copy FusionAuth from other image.
COPY --chown=fusionauth:fusionauth --from=build /usr/local/fusionauth /usr/local/fusionauth

###### Start FusionAuth App #########################################
LABEL description="Create an image running FusionAuth App. Installs FusionAuth App"
LABEL maintainer="FusionAuth-community <hopper.jerry@gmail.com>"
EXPOSE 9011
USER fusionauth
ENV FUSIONAUTH_USE_GLOBAL_JAVA=1
CMD ["/usr/local/fusionauth/fusionauth-app/apache-tomcat/bin/catalina.sh", "run"]

