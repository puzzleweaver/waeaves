
FROM ubuntu:latest

# Set environment variables for Webmin installation
ENV DEBIAN_FRONTEND=noninteractive

# Metadata as described above
LABEL maintainer="your_email@example.com" \
    version="1.1" \
    description="Dockerfile for running Webmin 1.920 on Ubuntu"

# TODO fix this lmao
RUN echo "root:root" | chpasswd

# Install basic dependencies with apt-get
RUN apt-get -y update && \
    apt-get -y install curl systemctl net-tools && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install webmin
RUN curl -o webmin-setup-repo.sh https://raw.githubusercontent.com/webmin/webmin/master/webmin-setup-repo.sh && \
    chmod +x webmin-setup-repo.sh && \
    yes | ./webmin-setup-repo.sh && \
    apt-get -y install --install-recommends webmin usermin

# Expose the default Webmin port
EXPOSE 10000

CMD ["systemctl", "start", "webmin.service"]
