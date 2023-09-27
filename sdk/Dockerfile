FROM ghcr.io/arifai/android-sdk:latest

LABEL org.opencontainers.image.source https://github.com/arifai/docker-flutter
LABEL org.opencontainers.image.description Flutter Docker image on Alpine Linux
LABEL org.opencontainers.image.licenses MIT

ARG FLUTTER_VERSION 3.13.5-stable

ENV ANDROID_USER android
ENV JAVA_HOME /usr/lib/jvm/java-21-openjdk
ENV PATH "$PATH:/$ANDROID_USER/flutter/bin:$JAVA_HOME/bin"

RUN set -eux; export JAVA_HOME=${JAVA_HOME}

RUN set -eux; addgroup -S ${ANDROID_USER} \ 
  && adduser \
  -h ${ANDROID_USER} \
  -S ${ANDROID_USER} \
  -G ${ANDROID_USER} -D

RUN set -eux; wget -q https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && tar xf flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && rm flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && mv flutter ${ANDROID_USER}

RUN set -eux; chown -R ${ANDROID_USER}:${ANDROID_USER} ${ANDROID_USER}

USER ${ANDROID_USER}

RUN set -eux; java -version \
  && yes | flutter doctor --android-licenses \
  && flutter config --no-analytics \
  && flutter doctor -v