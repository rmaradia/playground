FROM ubuntu:22.04

# Install required packages
RUN apt-get update && \
    apt-get install -y openssh-server sudo wget curl && \
    mkdir /var/run/sshd

# Create user and set password
RUN useradd -ms /bin/bash user && \
    echo 'user:password' | chpasswd && \
    usermod -aG sudo user && \
    echo 'user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set up root access and password
RUN echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Download and install Node Exporter
RUN wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz && \
    tar xvf node_exporter-1.8.1.linux-amd64.tar.gz && \
    mv node_exporter-1.8.1.linux-amd64/node_exporter /usr/local/bin/ && \
    rm -rf node_exporter*

# Expose SSH and node_exporter ports
EXPOSE 22 9100

# Start both sshd and node_exporter
CMD ["/bin/bash", "-c", "/usr/sbin/sshd && node_exporter"]

