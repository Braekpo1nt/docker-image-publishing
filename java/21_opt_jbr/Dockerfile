# Start from the official pterodactyl yolk for Java 21
FROM ghcr.io/pterodactyl/yolks:java_21

LABEL author="Braekpo1nt" \
      maintainer="braekpo1ntofficial@gmail.com" \
      description="Pterodactyl yolk with JBR alongside Eclipse Temurin 21" \
      org.opencontainers.image.description="Pterodactyl yolk with JBR alongside Eclipse Temurin 21" \
      org.opencontainers.image.source=https://github.com/Braekpo1nt/docker-image-publishing \
      org.opencontainers.image.licenses=MIT
# links this docker image to the gitlab repository where it came from, so that users can easily find information about it

USER root

# Install dependencies if not already present
RUN apt-get update -y \
    && apt-get install -y curl tar unzip ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Define a JBR version + download URL here for maintainability
ENV JBR_VERSION=jbr_jcef-21.0.7-linux-x64-b1038.58
ENV JBR_URL=https://cache-redirector.jetbrains.com/intellij-jbr/${JBR_VERSION}.tar.gz
ENV JBR_DIR=/opt/jbr

# Download and install JBR to JBR_DIR
RUN curl -fsSL "$JBR_URL" -o /tmp/jbr.tar.gz \
    && mkdir -p "$JBR_DIR" \
    && tar -xzf /tmp/jbr.tar.gz --strip-components=1 -C "$JBR_DIR" \
    && rm -f /tmp/jbr.tar.gz

# Show both Java runtimes available for inspection
RUN echo "Default java:" && java -version || true \
    && echo "JBR java:" && $JBR_DIR/bin/java -version || true

USER container
WORKDIR /home/container

CMD ["/bin/bash", "/entrypoint.sh"]
