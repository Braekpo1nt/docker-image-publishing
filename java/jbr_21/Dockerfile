FROM ghcr.io/pterodactyl/yolks:java_21

LABEL maintainer="braekpo1ntofficial@gmail.com"
LABEL description="Custom Pterodactyl yolk with JetBrains Runtime (JBR) as default Java to support hotswapping remote development."
# links this docker image to the gitlab repository where it came from, so that users can easily find information about it
LABEL org.opencontainers.image.source https://github.com/Braekpo1nt/docker-image-publishing

USER root

# Download and install JBR
ENV JBR_VERSION=jbr_jcef-21.0.7-linux-x64-b1038.58
ENV JBR_URL=https://cache-redirector.jetbrains.com/intellij-jbr/${JBR_VERSION}.tar.gz
ENV JBR_PATH=/usr/lib/jvm/jbr

RUN apt-get update && apt-get install -y wget tar \
  && wget -q ${JBR_URL} -O /tmp/jbr.tar.gz \
  && mkdir -p ${JBR_PATH} \
  && tar -xzf /tmp/jbr.tar.gz --strip-components=1 -C ${JBR_PATH} \
  && rm /tmp/jbr.tar.gz \
  # Point java & javac to JBR
  && update-alternatives --install /usr/bin/java java ${JBR_PATH}/bin/java 1 \
  && update-alternatives --install /usr/bin/javac javac ${JBR_PATH}/bin/javac 1 \
  && update-alternatives --set java ${JBR_PATH}/bin/java \
  && update-alternatives --set javac ${JBR_PATH}/bin/javac \
  && java -version

USER container

WORKDIR /home/container

CMD ["/bin/bash", "/entrypoint.sh"]
