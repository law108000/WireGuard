FROM --platform=linux/amd64 ubuntu:22.04

# update and install dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    unzip \
    vim \
    nano \
    sudo \
    iputils-ping \
    net-tools \
    iproute2 \
    iptables \
    dnsutils \
    iperf \
    iperf3 \
    nmap \
    tcpdump \
    traceroute \
    mtr \
    telnet \
    openssh-client \
    openssh-server \
    && rm -rf /var/lib/apt/lists/*

# install wireguard
RUN apt-get update && apt-get install -y wireguard-tools && rm -rf /var/lib/apt/lists/*

# start wireguard
# CMD ["wg-quick", "up", "wg0"]
CMD ["tail", "-f", "/dev/null"]
