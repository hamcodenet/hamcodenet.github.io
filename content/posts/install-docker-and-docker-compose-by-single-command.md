+++
title = 'Install Docker and Docker Compose by single command and use it without sudo :)'
date = 2023-09-08T00:00:00+00:00
draft = false
tags = ['docker', 'docker-compose', 'devops', 'linux', 'ansible']
+++

I know it looks crazy, but to be honest, I am frustrated with searching "install docker ubuntu" and copying and pasting lots of commands every time. If this happens to you a lot, you can bookmark [this gist](https://gist.github.com/hamidhaghdoost/b700f17f3ee3ad7f20d533e61de31c56) and just copy and paste it to install Docker, Compose, and post-installation commands.

```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done  &&
sudo apt-get update &&
sudo apt-get install ca-certificates curl gnupg &&
sudo install -m 0755 -d /etc/apt/keyrings &&
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg &&
sudo chmod a+r /etc/apt/keyrings/docker.gpg &&
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update &&
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin &&
sudo groupadd docker &&
sudo usermod -aG docker $USER &&
newgrp docker &&
sudo docker run hello-world
```

## A shorter way

If you don't want to copy such a long command, you can easily run this one:

```bash
 /bin/bash -c "$(curl -s https://gist.githubusercontent.com/hamidhaghdoost/b700f17f3ee3ad7f20d533e61de31c56/raw)"
```

It downloads the gist and runs the commands after getting the root password.

You can write an Ansible playbook as well to do the same:

```yaml
---
- name: Install Docker on Debian
  hosts: all
  become: true
  tasks:
    - name: Remove conflicting Docker packages
      apt:
        name: "{{ item }}"
        state: absent
        purge: true
      loop:
        - docker.io
        - docker-doc
        - docker-compose
        - podman-docker
        - containerd
        - runc
      ignore_errors: true

    - name: Update apt repository cache
      apt:
        update_cache: yes

    - name: Install prerequisite packages
      apt:
        name:
          - ca-certificates
          - curl
          - gnupg
        state: present

    - name: Create keyrings directory for Docker
      file:
        path: /etc/apt/keyrings
        state: directory
        mode: '0755'

    - name: Add Docker's official GPG key
      ansible.builtin.command:
        cmd: curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      args:
        creates: /etc/apt/keyrings/docker.gpg

    - name: Set permissions for Docker GPG key
      file:
        path: /etc/apt/keyrings/docker.gpg
        mode: '0644'

    - name: Add Docker repository
      ansible.builtin.apt_repository:
        repo: "deb [arch={{ ansible_architecture }} signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian {{ ansible_lsb.codename }} stable"
        filename: docker

    - name: Update apt cache after adding Docker repo
      apt:
        update_cache: yes

    - name: Install Docker packages
      apt:
        name:
          - docker-ce
          - docker-ce-cli
          - containerd.io
          - docker-buildx-plugin
          - docker-compose-plugin
        state: present

    - name: Create Docker group if it does not exist
      group:
        name: docker
        state: present

    - name: Add user to Docker group
      user:
        name: "{{ ansible_user }}"
        groups: docker
        append: yes

    - name: Run Docker hello-world to verify installation
      command: docker run hello-world
      register: docker_test_result
      failed_when: docker_test_result.rc != 0
```

Ciao e buon week-end :)
