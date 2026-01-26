# Use production image as base to avoid duplication
ARG REACT_APP_INTELOWL_VERSION=stag
FROM intelowlproject/intelowl:${REACT_APP_INTELOWL_VERSION}

# Switch to root to install development tools
USER root

# Install git + essentials
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    # FIXME: install docker-buildx-plugin
    git curl wget gnupg ca-certificates lsb-release && \
    install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    chmod a+r /etc/apt/keyrings/docker.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y --no-install-recommends docker-ce-cli && \
    curl -fsSL https://opencode.ai/install | bash && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /tmp/* /var/tmp/* /etc/apt/keyrings/docker.gpg



# Install debugpy for development debugging
RUN pip3 install --no-cache-dir debugpy

# Fix www-data user for DevContainer compatibility
# Production image creates www-data with UID 33, GID 33
# VS Code remaps to 1000:1000, so we need to update the UID/GID
RUN groupadd -g 988 docker && \
    usermod -aG docker www-data && \
    mkdir -p /home/www-data && \
    chown -R 1000:1000 /home/www-data /var/log/intel_owl /opt/deploy/

# Switch back to www-data user
ENV HOME=/home/www-data
USER www-data

# Expose debugging port
EXPOSE 5678

# Default command for development
CMD ["sleep", "infinity"]