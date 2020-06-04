# This Dockerfile uses multi-stage builds. The prep stage is used
# to prepare any needed files for use in the final image. This avoids
# having to do cleanup inside of steps in the final image.
ARG APP_NAME_ARG=ddf-demo
ARG PROJECT_VERSION_ARG=2.23.0
ARG DISTRIBUTION_ARG=${APP_NAME_ARG}-${PROJECT_VERSION_ARG}.zip
ARG DOCKER_DDF_BASE_VERSION_ARG=2.14-alpine

# Prep Stage
FROM alpine as prep

# No longer need this as unzip is included in busybox - we include if busybox/unzip is not complete
# RUN apk add --no-cache unzip
RUN mkdir /prep /zips
ARG APP_NAME_ARG
ARG PROJECT_VERSION_ARG
#COPY ${APP_NAME_ARG}-${PROJECT_VERSION_ARG}.zip /zips
COPY target/dependency/${APP_NAME_ARG}-${PROJECT_VERSION_ARG}.zip /zips
ARG APP_NAME_ARG
ARG PROJECT_VERSION_ARG
RUN unzip /zips/${APP_NAME_ARG}-${PROJECT_VERSION_ARG}.zip -d /prep
ARG APP_NAME_ARG
ARG PROJECT_VERSION_ARG
RUN mv /prep/${APP_NAME_ARG}-${PROJECT_VERSION_ARG} /prep/${APP_NAME_ARG}

# Final Image Stage
ARG DOCKER_DDF_BASE_VERSION_ARG
FROM codice/ddf-base:${DOCKER_DDF_BASE_VERSION_ARG}
LABEL maintainer=codice

ARG APP_NAME_ARG
ENV APP_HOME=/app
ENV APP_NAME=/${APP_NAME_ARG}
ENV APP_LOG=$APP_HOME/data/log/ddf.log

COPY --from=prep /prep/$APP_NAME $APP_HOME

VOLUME $APP_HOME/data $APP_HOME/deploy $APP_HOME/etc

EXPOSE 8993 8181 8101
