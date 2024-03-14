ARG VARIANT="3.2.3-slim"
ARG NODE_VERSION="14"
FROM ruby:${VARIANT}

ARG DEV_PACKAGES="build-essential"

# Update the package lists and install Node.js
RUN apt-get update && \
    curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - && \
    apt-get install --no-install-recommends -y nodejs && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Optionally set a non-root user
RUN groupadd --gid 1000 node \
    && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

# hadolint ignore=SC2086,DL3008
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y ${DEV_PACKAGES} && \
    gem install bundler jekyll && \
    apt-get remove --purge -y $DEV_PACKAGES && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog

# Set the default shell to bash instead of sh
ENV SHELL /bin/bash


