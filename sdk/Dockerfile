FROM ghcr.io/arifai/android-sdk:latest

LABEL org.opencontainers.image.source https://github.com/arifai/docker-flutter
LABEL org.opencontainers.image.description Docker Image for Flutter
LABEL org.opencontainers.image.licenses MIT

ARG FLUTTER_VERSION

ENV ANDROID_USER android
ENV PATH "$PATH:/$ANDROID_USER/flutter/bin"

RUN addgroup -S ${ANDROID_USER} \ 
  && adduser \
  -h ${ANDROID_USER} \
  -S ${ANDROID_USER} \
  -G ${ANDROID_USER} -D

RUN wget -q https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && tar xf flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && rm flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && mv flutter ${ANDROID_USER}

RUN chown -R ${ANDROID_USER}:${ANDROID_USER} ${ANDROID_USER}

USER ${ANDROID_USER}

RUN yes | flutter doctor --android-licenses \
  && flutter doctor