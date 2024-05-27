FROM ghcr.io/arifai/android-sdk:latest

ARG FLUTTER_VERSION
ARG FLUTTER_CHANNEL

LABEL io.github.arifai.image.souce https://github.com/arifai/docker-flutter
LABEL io.github.arifai.image.version ${FLUTTER_VERSION}
LABEL org.opencontainers.image.source https://github.com/arifai/docker-flutter
LABEL org.opencontainers.image.description Flutter Docker image on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

ENV ANDROID_USER android
ENV ANDROID_DIR /home/${ANDROID_USER}
ENV PATH "$PATH:$ANDROID_DIR/flutter/bin"

WORKDIR ${ANDROID_DIR}

RUN set -eux; groupadd -r ${ANDROID_USER} \
  && useradd -r -g ${ANDROID_USER} ${ANDROID_USER}

RUN set -eux; apt-get update && apt-get upgrade -y \ 
  && apt-get install clang cmake ninja-build pkg-config -y --no-install-recommends \
  && curl https://storage.googleapis.com/flutter_infra_release/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz -o flutter.tar.xz \
  && tar xf flutter.tar.xz \
  && rm flutter.tar.xz \
  && chown -R ${ANDROID_USER}:${ANDROID_USER} ${ANDROID_DIR}

USER ${ANDROID_USER}

RUN set -eux; yes | flutter doctor --android-licenses \
  && flutter config --no-analytics \
  && flutter doctor -v