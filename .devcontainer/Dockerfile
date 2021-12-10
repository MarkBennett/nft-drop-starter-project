# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.203.0/containers/rust/.devcontainer/base.Dockerfile

# [Choice] Debian OS version (use bullseye on local arm64/Apple Silicon): buster, bullseye
ARG VARIANT="buster"
FROM mcr.microsoft.com/vscode/devcontainers/rust:0-${VARIANT}

# Replace the default shell with bash
SHELL ["/bin/bash", "-l", "-euxo", "pipefail", "-c"]

# install nvm
ENV NVM_DIR /usr/local/nvm
ARG NODE_VERSION=17.2.0

RUN mkdir -p "$NVM_DIR" \
    && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

RUN source $NVM_DIR/nvm.sh \
    && nvm install ${NODE_VERSION} \
    && nvm alias default ${NODE_VERSION} \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# Install ts-node as we'll need it for this example
RUN npm install -g ts-node

# Install Solana
ENV SOLANA_PATH /usr/local/solana
ENV SOLANA_RELEASE v1.8.5
RUN mkdir -p $SOLANA_PATH
RUN cd $SOLANA_PATH && \
    curl -L --output ./solana.tar.bz2 https://github.com/solana-labs/solana/releases/download/$SOLANA_RELEASE/solana-release-x86_64-unknown-linux-gnu.tar.bz2
RUN cd $SOLANA_PATH && \
    tar jxf ./solana.tar.bz2
ENV PATH $SOLANA_PATH/solana-release/bin:$PATH

RUN command -v nvm; \
    command -v node; \
    node --version; \
    command -v npm; \
    npm --version

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
