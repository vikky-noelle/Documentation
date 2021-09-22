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

<pre>
CONTAINER ID   IMAGE                COMMAND                  CREATED       STATUS                     PORTS     NAMES
7fe30c11f67a   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      5 days ago    Exited (0) 5 days ago                modest_johnson
0d59fd818862   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      5 days ago    Exited (0) 5 days ago                lucid_keller
ecd348a1ba7b   ubuntu-ssh-enabled   "/usr/sbin/sshd -D"      6 days ago    Exited (0) 5 days ago                amazing_margulis
efd8ef1825b1   ansible              "bash"                   6 days ago    Exited (0) 5 days ago                admiring_khayyam
1fc9ffd0b899   mysql:5.7            "docker-entrypoint.s…"   3 weeks ago   Exited (0) 3 weeks ago               db
e125f04f088e   remote-host          "/bin/sh -c '/usr/sb…"   3 weeks ago   Exited (0) 3 weeks ago               remote-host
1e1d296f7260   jenkins/jenkins      "/sbin/tini -- /usr/…"   4 weeks ago   Exited (143) 3 weeks ago             jenkins
fa06aac73673   my-simple-webapp     "/bin/sh -c 'FLASK_A…"   5 weeks ago   Exited (137) 5 weeks ago             stupefied_swanson
a1a69e54319a   ubuntu               "bash"                   5 weeks ago   Exited (0) 5 weeks ago               great_ellis
77c13ddf8a64   ubuntu               "bash"                   5 weeks ago   Exited (0) 5 weeks ago               infallible_mclaren
1304d07ea25e   ubuntu               "bash"                   5 weeks ago   Exited (0) 5 weeks ago               epic_morse
</pre>
