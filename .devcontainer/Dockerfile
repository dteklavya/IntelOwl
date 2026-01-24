# Use production image as base to avoid duplication
FROM intelowlproject/intelowl:prod

# Switch to root to install development tools
USER root

# Install git + essentials (Alpine = apk)
RUN apk add --no-cache \
    git curl wget ca-certificates docker-cli && \
    curl -fsSL https://opencode.ai/install | bash && \
    rm -rf /var/cache/apk/*


# Install debugpy for development debugging
RUN pip3 install --no-cache-dir debugpy

# Fix www-data user for DevContainer compatibility
# Production image creates www-data with UID 2000, GID 65533, no home directory
# VS Code needs to remap to 1000:1000, so we need to create a proper home directory
RUN mkdir -p /home/www-data \
    && chown 2000:65533 /home/www-data \
    && echo 'www-data:x:2000:65533::/home/www-data:/bin/sh' >> /etc/passwd

# Switch back to www-data user
USER www-data

# Expose debugging port
EXPOSE 5678

# Default command for development
CMD ["sleep", "infinity"]