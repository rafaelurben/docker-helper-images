# Docker Helper Images

This repository contains a collection of Docker helper images that can be used as base images or utility images in various Docker-based projects. Each image is designed to perform specific tasks or provide certain functionalities to enhance the Docker ecosystem.

## Available Images

- **jenkins-agent**: A Docker image for running Jenkins agents.
  - Extends `jenkins/agent:bookwork-jdk21`
  - Includes additional tools: `mvn`, `nodejs`, `npm`, `wget`, `unzip`, `gnupg2`, `sonar-scanner`, `jmeter`, `google-chrome`, `docker` (and `docker scout`).
  - [Dockerfile](./jenkins-agent/Dockerfile)
  - [GitHub Container Registry](https://github.com/users/rafaelurben/packages/container/package/jenkins-agent)
  - Image: `ghcr.io/rafaelurben/jenkins-agent:latest`
