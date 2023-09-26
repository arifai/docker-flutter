FROM android-sdk:latest

LABEL io.github.arifai.images.souce=https://github.com/arifai/docker-flutter

ARG FLUTTER_VERSION

ENV FLUTTER_HOME ${HOME}/Flutter/Sdk
ENV PATH "$PATH:$FLUTTER_HOME/flutter/bin"

RUN git config --global --add safe.directory ${FLUTTER_HOME}/flutter \
  && wget -q https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && tar xf flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && rm flutter_linux_${FLUTTER_VERSION}.tar.xz \
  && mkdir -p ${FLUTTER_HOME} \
  && mv flutter ${FLUTTER_HOME}

RUN yes | flutter doctor --android-licenses \
  && flutter doctor