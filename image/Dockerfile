FROM jenkins/jenkins:2.401.2-lts-jdk11

# environment initialization
USER root

ARG DOCKER_CREDENTIAL_ECR_LOGIN_VERSION="0.7.1"
ARG BLUEOCEAN_VERSION="1.27.5"
ARG DOCKER_WORKFLOW_VERSION="563.vd5d2e5c4007f"

RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
    https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
    signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
    https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli

RUN curl -fsSLo /usr/bin/docker-credential-ecr-login \
    https://amazon-ecr-credential-helper-releases.s3.us-east-2.amazonaws.com/${DOCKER_CREDENTIAL_ECR_LOGIN_VERSION}/linux-amd64/docker-credential-ecr-login && \
    curl -fsSLo /tmp/docker-credential-ecr-login.sha256 \
    https://amazon-ecr-credential-helper-releases.s3.us-east-2.amazonaws.com/${DOCKER_CREDENTIAL_ECR_LOGIN_VERSION}/linux-amd64/docker-credential-ecr-login.sha256 && \
    cd /usr/bin/ && sha256sum -c /tmp/docker-credential-ecr-login.sha256 && \
    chmod +x /usr/bin/docker-credential-ecr-login

# add extended dockerfile file
RUN mkdir /dockerfile
ADD ./extra_dockerfile /dockerfile

# plugin Installation
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:${BLUEOCEAN_VERSION} docker-workflow:${DOCKER_WORKFLOW_VERSION}"

