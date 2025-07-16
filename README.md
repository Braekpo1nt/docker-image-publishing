# docker-image-publishing
Used to upload my custom docker images to the ghcr.io (GitHub container registry)

I learned how to create this repository from this video: https://www.youtube.com/watch?v=RgZyX-e6W9E

# Naming and versioning scheme

Docker images published using this repository are published to the GitHub Container Registry (ghcr.io) under the owner of this repo (Braekpo1nt) using the name `yolks` with the version of `<dir>_<sub_dir>` where `<dir>` is the top-level folder from repository `<root>` and `<sub_dir>` is the specific folder in that `<dir>` with a `Dockerfile` in it. For example, [root/java/jbr_21/Dockerfile](./java/jbr_21/Dockerfile) is published under `ghcr.io/braekpo1nt/yolks:java_jbr_21`.

# Usage

To use them, copy the identifier into your server's **Startup>Docker Image Configuration>Image** setting.
