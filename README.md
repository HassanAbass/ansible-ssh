# My Project README

## Prerequisites

Before you can get started with this project, ensure you have the following prerequisites in place:

- Docker
- Ansible

### Copying Public Key to Target Container

To copy your public key to a target container for SSH authentication, follow these steps:

1. Build Docker image with ssh installed on it
   ```bash
   docker build -t ubuntu-ssh .
2. run container with port open for ssh and apache
   ```bash
   docker run -d -p 2220:22 ubuntu-ssh
   docker run -d -p 2221:22 ubuntu-ssh
   docker run -d -p 2222:22 ubuntu-ssh
3. Generate an SSH key pair (public and private keys) if you don't already have one:
   ```bash
   ssh-keygen -t ed25591 -C "user@example.com"
4. Copy SSH key pair into docker containers so ansible can access them(**password** provided in Dockerfile):
   ```bash
   ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2220 root@localhost
   ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2221 root@localhost
   ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2222 root@localhost

### Usage

1. Run ansible to configure packages containers
   ```bash
   ansible-playbook install_apache.yml
