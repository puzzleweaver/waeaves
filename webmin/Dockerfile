
FROM ubuntu:latest

# Metadata as described above
LABEL maintainer="emma.e.weaver1@gmail.com" \
    version="1.2" \
    description="Dockerfile for running Webmin on Ubuntu"

RUN --mount=type=secret,id=webmin_password,env=WEBMIN_PASSWORD \
    echo "root:$WEBMIN_PASSWORD" | chpasswd

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
