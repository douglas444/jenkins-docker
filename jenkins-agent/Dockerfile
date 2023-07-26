FROM jenkins/ssh-agent:jdk11

# Java for building the application
ENV JAVA_HOME=/opt/java/openjdk
COPY --from=eclipse-temurin:latest $JAVA_HOME $JAVA_HOME
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Update package lists and install necessary tools
RUN apt-get update && \
    apt-get -y --no-install-recommends install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common

# Add Docker's official GPG key
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey && \
    apt-key add /tmp/dkey

# Add Docker's official repository
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable"

# Install Docker CE
RUN apt-get update && \
    apt-get -y --no-install-recommends install docker-ce

#Install other dependencies
RUN apt-get install docker-compose-plugin -y
RUN apt-get install git -y

# Clean up APT cache to reduce image size
RUN apt-get clean

#Give jenkins user access to the docker group
RUN usermod -a -G docker jenkins