# Use Ubuntu 22.04 as the base image
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic tools
RUN apt-get update && apt-get install -y \
    sudo \
    curl \
    wget \
    git \
    unzip \
    gnupg2 \
    software-properties-common \
    lsb-release \
    net-tools \
    apt-transport-https \
    ca-certificates

# Install Java 11
RUN apt-get install -y openjdk-11-jdk

# Install Maven
RUN apt-get install -y maven

# Install Docker CLI (for Docker-in-Docker use)
RUN apt-get install -y docker.io

# Install Jenkins
RUN curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null && \
    echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null && \
    apt-get update && \
    apt-get install -y jenkins

# Download and prepare Nexus
RUN mkdir -p /opt/nexus && \
    cd /opt/nexus && \
    wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz && \
    tar -xzf latest-unix.tar.gz && \
    rm latest-unix.tar.gz && \
    mv nexus-* nexus && \
    adduser --system --no-create-home --group nexus && \
    chown -R nexus:nexus /opt/nexus

# Set environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH
