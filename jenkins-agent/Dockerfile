# Use Debian Bookworm base image with OpenJDK 21
FROM jenkins/agent:bookworm-jdk21

USER root

# Install additional tools: Maven, Node.js, npm, wget, unzip, gnupg2, ca-certificates, curl, uidmap, iproute2, jq
RUN apt-get update -qq && apt-get install -y -qq maven nodejs npm wget unzip gnupg2 ca-certificates curl uidmap iproute2 jq

# Install Sonar Scanner
RUN wget -q https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.2.0.5079-linux-x64.zip -O /tmp/sonar-scanner.zip && \
    unzip -q /tmp/sonar-scanner.zip -d /tmp/sonar-scanner && \
    mv /tmp/sonar-scanner/sonar-scanner-7.2.0.5079-linux-x64 /opt/sonar-scanner
ENV PATH="${PATH}:/opt/sonar-scanner/bin"
# Install JMeter
RUN wget -q https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-5.6.3.tgz -O /tmp/jmeter.tgz && \
    tar -xzf /tmp/jmeter.tgz -C /opt/ && \
    mv /opt/apache-jmeter-5.6.3 /opt/jmeter && \
    rm /tmp/jmeter.tgz
ENV PATH="${PATH}:/opt/jmeter/bin"
# Install Google Chrome
RUN wget -qO - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo 'deb [arch=amd64] https://dl.google.com/linux/deb/ stable main' > /etc/apt/sources.list.d/google.list && \
    apt-get update -qq && apt-get install -y -qq google-chrome-stable && \
    google-chrome --version

# Install Docker
RUN install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc && \
    echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian $(. /etc/os-release && echo "$VERSION_CODENAME") stable" > /etc/apt/sources.list.d/docker.list && \
    apt-get update -qq && apt-get install -y -qq docker-ce docker-ce-cli containerd.io docker-buildx-plugin && \
    docker --version

# Clean up
RUN apt-get clean && rm -rf /tmp/* /var/tmp/*
# Switch back to the jenkins user
USER jenkins

# Install Docker Scout
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh -o install-scout.sh)" && \
    mkdir ~/.docker && \
    sh install-scout.sh && \
    rm install-scout.sh && \
    docker scout version
