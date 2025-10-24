# Use Debian Bookworm base image with OpenJDK 21
FROM jenkins/agent:bookworm-jdk21

USER root

# Install additional tools: Maven, Node.js, npm, wget, unzip, gnupg2
RUN apt-get update && apt-get install -y maven nodejs npm wget unzip gnupg2

# Install Sonar Scanner
RUN wget -q https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.2.0.5079-linux-x64.zip -O /tmp/sonar-scanner.zip && \
    unzip /tmp/sonar-scanner.zip -d /tmp/sonar-scanner && \
    mv /tmp/sonar-scanner/sonar-scanner-7.2.0.5079-linux-x64 /opt/sonar-scanner
ENV PATH="${PATH}:/opt/sonar-scanner/bin"
# Install JMeter
RUN wget -q https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-5.6.3.tgz -O /tmp/jmeter.tgz && \
    tar -xzf /tmp/jmeter.tgz -C /opt/ && \
    mv /opt/apache-jmeter-5.6.3 /opt/jmeter
ENV PATH="${PATH}:/opt/jmeter/bin"
# Install Google Chrome
RUN wget -qO - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo 'deb [arch=amd64] https://dl.google.com/linux/deb/ stable main' > /etc/apt/sources.list.d/google.list && \
    apt-get update && apt-get install -y google-chrome-stable && \
    google-chrome --version

# Clean up
RUN apt-get clean && rm -rf /tmp/* /var/tmp/*
# Switch back to the jenkins user
USER jenkins
