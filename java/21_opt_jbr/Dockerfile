# Start from the official pterodactyl yolk for Java 21
FROM ghcr.io/pterodactyl/yolks:java_21

LABEL author="Braekpo1nt"
LABEL maintainer="braekpo1ntofficial@gmail.com"
LABEL description="Pterodactyl yolk with JBR alongside Eclipse Temurin 21"
# links this docker image to the gitlab repository where it came from, so that users can easily find information about it
LABEL org.opencontainers.image.description="Pterodactyl yolk with JBR alongside Eclipse Temurin 21"
LABEL org.opencontainers.image.source=https://github.com/Braekpo1nt/docker-image-publishing
LABEL org.opencontainers.image.licenses=MIT

USER root

ENV JBR_VERSION=jbr-21.0.7-linux-x64-b659.16 \
    JBR_DIR=/opt/jbr \
    JBR_URL=https://cache-redirector.jetbrains.com/intellij-jbr/${JBR_VERSION}.tar.gz

# install JetBrains Runtime (JBR) for optional use
RUN mkdir -p "${JBR_DIR}" \
 && curl -fsSL "${JBR_URL}" -o /tmp/jbr.tar.gz \
 && tar -xzf /tmp/jbr.tar.gz -C "${JBR_DIR}" --strip-components=1 \
 && rm /tmp/jbr.tar.gz \
 && rm -rf /var/lib/apt/lists/* \
 && ${JBR_DIR}/bin/java --version \
 && java --version

USER ${USER}
WORKDIR ${HOME}
