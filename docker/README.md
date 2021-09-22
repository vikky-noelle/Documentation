# Docker

## Introduction

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

## Docker Architecture

![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)

## Commands and use

- `docker ps`
  This command is used to see the containers running currently.

- `docker ps -a`
  This command is used to see the containers that were running in the past.

- `docker ps` command output looks like this.

    <pre>
    CONTAINER ID   IMAGE                COMMAND                  CREATED       STATUS                     PORTS     NAMES
    7fe30c11f67a   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      5 days ago    Exited (0) 5 days ago                modest_johnson
    0d59fd818862   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      5 days ago    Exited (0) 5 days ago                lucid_keller
    ecd348a1ba7b   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      6 days ago    Exited (0) 5 days ago                amazing_margulis
    </pre>

  `CONTAINER ID` is a unique string that is assigned to each container.

  `IMAGE` is the image on which the container is based.

  **Note that multiple containers can have the same image.**
