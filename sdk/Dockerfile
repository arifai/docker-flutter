FROM ghcr.io/arifai/android-sdk:latest

LABEL org.opencontainers.image.source https://github.com/arifai/docker-flutter
LABEL org.opencontainers.image.description Docker Image for Flutter
LABEL org.opencontainers.image.licenses MIT

ARG FLUTTER_VERSION

ENV FLUTTER_USER flutter

RUN addgroup -S ${FLUTTER_USER} \ 
  && adduser \
  -S ${FLUTTER_USER} \
  -G ${FLUTTER_USER} \
  -D -H

ENV FLUTTER_HOME ${HOME}/Flutter/Sdk
ENV PATH "$PATH:$FLUTTER_HOME/flutter/bin"

RUN git config --global --add safe.directory ${FLUTTER_HOME}/flutter \
  && mkdir -p ${FLUTTER_HOME} \
  && wget -q https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && tar xf flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && rm flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && mv flutter ${FLUTTER_HOME} \
  && rm -rf ${FLUTTER_HOME}/flutter/bin/cache

RUN chown ${FLUTTER_USER}:${FLUTTER_USER} ${FLUTTER_HOME}

RUN yes | flutter doctor --android-licenses \
  && flutter doctor