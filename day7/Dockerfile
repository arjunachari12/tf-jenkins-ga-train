FROM jenkins/jenkins:2.492.2-jdk17

USER root

# Install required dependencies
RUN apt-get update && apt-get install -y \
    lsb-release \
    unzip \
    curl \
    awscli \
    jq

# Install Docker CLI (already present in your config)
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli

# Install Terraform
RUN curl -fsSL https://releases.hashicorp.com/terraform/1.6.0/terraform_1.6.0_linux_amd64.zip -o terraform.zip \
    && unzip terraform.zip \
    && mv terraform /usr/local/bin/ \
    && rm -rf terraform.zip \
    && terraform --version

# Switch back to Jenkins user
USER jenkins

# Install necessary Jenkins plugins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"
