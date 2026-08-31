# Java 21 LTS development-container image
FROM mcr.microsoft.com/devcontainers/java:21-bookworm

ENV DEBIAN_FRONTEND=noninteractive
ENV FLUTTER_HOME=/opt/flutter
ENV PATH="${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin:${PATH}"


# Install Maven and dependencies used by Flutter
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        clang \
        cmake \
        curl \
        git \
        libglu1-mesa \
        libgtk-3-dev \
        make \
        maven \
        ninja-build \
        pkg-config \
        unzip \
        wget \
        xz-utils \
        zip \
    && rm -rf /var/lib/apt/lists/*

# Install the stable Flutter SDK
RUN git clone \
        --depth 1 \
        --branch stable \
        https://github.com/flutter/flutter.git \
        "${FLUTTER_HOME}" \
    && chown -R vscode:vscode "${FLUTTER_HOME}"


USER vscode

# Enable and download Flutter Web components
RUN flutter config --enable-web \
    && flutter precache --web \
    && flutter --version

WORKDIR /workspace

EXPOSE 8080

CMD ["/bin/bash"]