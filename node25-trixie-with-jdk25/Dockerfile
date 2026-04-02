# Use Node.js 25 Trixie base image
FROM node:25-trixie

# Install OpenJDK 25 headless
RUN apt-get update -qq && apt-get install -y -qq openjdk-25-jdk-headless && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
