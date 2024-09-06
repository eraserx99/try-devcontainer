FROM "mcr.microsoft.com/devcontainers/java:21-jdk-bookworm"

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install git

# ENV SDKMAN_DIR="/usr/local/sdkman"
# ENV PATH=${SDKMAN_DIR}/bin:${SDKMAN_DIR}/candidates/gradle/current/bin:${PATH}
# COPY library-scripts/gradle-debian.sh /tmp/library-scripts/
# RUN apt-get update && bash /tmp/library-scripts/gradle-debian.sh "latest" "${SDKMAN_DIR}"

