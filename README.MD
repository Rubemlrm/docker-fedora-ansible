# Fedora Ansible Test Images

[![CI](https://github.com/Rubemlrm/docker-fedora-ansible/workflows/Build/badge.svg?branch=master&event=push)](https://github.com/Rubemlrm/docker-fedora-ansible/actions?query=workflow%3ABuild)

Fedora Docker containers for Ansible playbook and role testing.


## Important Notes

Based on the work created by [Jeff Geerling](https://www.jeffgeerling.com/). I'm just using the base dockerFile that Jeff created and applying to the new versions of fedora including the testing ones. The ideia and the main work was made by him, so if you want, support him.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `main` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t fedora<version>-ansible <dockerFile>`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull rubemlrm/fedora35-ansible:latest` (or use the image you built earlier, e.g. `fedora35-ansible:latest`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro rubemlrm/fedora34-ansible:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`
