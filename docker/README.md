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

  `COMMAND` is the command that is running after the image is built.

- `docker images`
  This command is used to see the images in the local environment, images can be from docker hub or images built.

- `docker inspect CONTAINER ID`
  This command is used to see information associated with a container or an image.

- `docker run [OPTIONS] IMAGE NAME [COMMAND] [ARG...]`
  This command is used to run images in the form of containers.

  **Note, docker run without `-t` is a container that does not have terminal drivers, hence it will fail to run terminal in such containers when you do a start. Containers that need bash should be run with `-t` tag.**

  Options:

    <pre>
    --add-host list Add a custom host-to-IP mapping (host:ip)
    -a, --attach list Attach to STDIN, STDOUT or STDERR
    --blkio-weight uint16 Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
    --blkio-weight-device list Block IO weight (relative device weight) (default [])
    --cap-add list Add Linux capabilities
    --cap-drop list Drop Linux capabilities
    --cgroup-parent string Optional parent cgroup for the container
    --cgroupns string Cgroup namespace to use (host|private)
    'host': Run the container in the Docker host's cgroup namespace
    'private': Run the container in its own private cgroup namespace
    '': Use the cgroup namespace as configured by the
    default-cgroupns-mode option on the daemon (default)
    --cidfile string Write the container ID to the file
    --cpu-period int Limit CPU CFS (Completely Fair Scheduler) period
    --cpu-quota int Limit CPU CFS (Completely Fair Scheduler) quota
    --cpu-rt-period int Limit CPU real-time period in microseconds
    --cpu-rt-runtime int Limit CPU real-time runtime in microseconds
    -c, --cpu-shares int CPU shares (relative weight)
    --cpus decimal Number of CPUs
    --cpuset-cpus string CPUs in which to allow execution (0-3, 0,1)
    --cpuset-mems string MEMs in which to allow execution (0-3, 0,1)
    -d, --detach Run container in background and print container ID
    --detach-keys string Override the key sequence for detaching a container
    --device list Add a host device to the container
    --device-cgroup-rule list Add a rule to the cgroup allowed devices list
    --device-read-bps list Limit read rate (bytes per second) from a device (default [])
    --device-read-iops list Limit read rate (IO per second) from a device (default [])
    --device-write-bps list Limit write rate (bytes per second) to a device (default [])
    --device-write-iops list Limit write rate (IO per second) to a device (default [])
    --disable-content-trust Skip image verification (default true)
    --dns list Set custom DNS servers
    --dns-option list Set DNS options
    --dns-search list Set custom DNS search domains
    --domainname string Container NIS domain name
    --entrypoint string Overwrite the default ENTRYPOINT of the image
    -e, --env list Set environment variables
    --env-file list Read in a file of environment variables
    --expose list Expose a port or a range of ports
    --gpus gpu-request GPU devices to add to the container ('all' to pass all GPUs)
    --group-add list Add additional groups to join
    --health-cmd string Command to run to check health
    --health-interval duration Time between running the check (ms|s|m|h) (default 0s)
    --health-retries int Consecutive failures needed to report unhealthy
    --health-start-period duration Start period for the container to initialize before starting health-retries countdown (ms|s|m|h) (default 0s)
    --health-timeout duration Maximum time to allow one check to run (ms|s|m|h) (default 0s)
    --help Print usage
    -h, --hostname string Container host name
    --init Run an init inside the container that forwards signals and reaps processes
    -i, --interactive Keep STDIN open even if not attached
    --ip string IPv4 address (e.g., 172.30.100.104)
    --ip6 string IPv6 address (e.g., 2001:db8::33)
    --ipc string IPC mode to use
    --isolation string Container isolation technology
    --kernel-memory bytes Kernel memory limit
    -l, --label list Set meta data on a container
    --label-file list Read in a line delimited file of labels
    --link list Add link to another container
    --link-local-ip list Container IPv4/IPv6 link-local addresses
    --log-driver string Logging driver for the container
    --log-opt list Log driver options
    --mac-address string Container MAC address (e.g., 92:d0:c6:0a:29:33)
    -m, --memory bytes Memory limit
    --memory-reservation bytes Memory soft limit
    --memory-swap bytes Swap limit equal to memory plus swap: '-1' to enable unlimited swap
    --memory-swappiness int Tune container memory swappiness (0 to 100) (default -1)
    --mount mount Attach a filesystem mount to the container
    --name string Assign a name to the container
    --network network Connect a container to a network
    --network-alias list Add network-scoped alias for the container
    --no-healthcheck Disable any container-specified HEALTHCHECK
    --oom-kill-disable Disable OOM Killer
    --oom-score-adj int Tune host's OOM preferences (-1000 to 1000)
    --pid string PID namespace to use
    --pids-limit int Tune container pids limit (set -1 for unlimited)
    --platform string Set platform if server is multi-platform capable
    --privileged Give extended privileges to this container
    -p, --publish list Publish a container's port(s) to the host
    -P, --publish-all Publish all exposed ports to random ports
    --pull string Pull image before running ("always"|"missing"|"never") (default "missing")
    --read-only Mount the container's root filesystem as read only
    --restart string Restart policy to apply when a container exits (default "no")
    --rm Automatically remove the container when it exits
    --runtime string Runtime to use for this container
    --security-opt list Security Options
    --shm-size bytes Size of /dev/shm
    --sig-proxy Proxy received signals to the process (default true)
    --stop-signal string Signal to stop a container (default "SIGTERM")
    --stop-timeout int Timeout (in seconds) to stop a container
    --storage-opt list Storage driver options for the container
    --sysctl map Sysctl options (default map[])
    --tmpfs list Mount a tmpfs directory
    -t, --tty Allocate a pseudo-TTY
    --ulimit ulimit Ulimit options (default [])
    -u, --user string Username or UID (format: <name|uid>[:<group|gid>])
    --userns string User namespace to use
    --uts string UTS namespace to use
    -v, --volume list Bind mount a volume
    --volume-driver string Optional volume driver for the container
    --volumes-from list Mount volumes from the specified container(s)
    -w, --workdir string Working directory inside the container
  </pre>

  **Note that multiple run on the same image creates multiple unique containers.**

  **Note that run is exclusively used for images and will give you an error if you try it with a container.**

- `docker start/stop CONTAINER ID`
  This command is used to start or stop a container.

  **Note, this command is exclusive to containers.**

- `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`
  This command runs a new command on a running container.

  e.g `docker exec -ti my_container bash` will start the bash on the container, given that it exists.
  Consider bash similar to terminal in linux based systems.

  Options:

    <pre>
    -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a container
    -e, --env list             Set environment variables
      --env-file list        Read in a file of environment variables
    -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
    -t, --tty                  Allocate a pseudo-TTY
    -u, --user string          Username or UID (format: <name|uid>[:<group|gid>])
    -w, --workdir string       Working directory inside the container
    </pre>

- `docker info`
  This command displays system wide information.

- `docker attach [OPTIONS] CONTAINER ID`
  Attach local standard input, output, and error streams to a running container.

  Options:

    <pre>
      --detach-keys string   Override the key sequence for detaching a container
      --no-stdin             Do not attach STDIN
      --sig-proxy            Proxy all received signals to the process (default true)
    </pre>

- `docker build [OPTIONS] PATH | URL | -`
  Build an image from a docker file.

  Options:

    <pre>
        --add-host list           Add a custom host-to-IP mapping (host:ip)
        --build-arg list          Set build-time variables
        --cache-from strings      Images to consider as cache sources
        --cgroup-parent string    Optional parent cgroup for the container
        --compress                Compress the build context using gzip
        --cpu-period int          Limit the CPU CFS (Completely Fair Scheduler) period
        --cpu-quota int           Limit the CPU CFS (Completely Fair Scheduler) quota
    -c, --cpu-shares int          CPU shares (relative weight)
        --cpuset-cpus string      CPUs in which to allow execution (0-3, 0,1)
        --cpuset-mems string      MEMs in which to allow execution (0-3, 0,1)
        --disable-content-trust   Skip image verification (default true)
    -f, --file string             Name of the Dockerfile (Default is 'PATH/Dockerfile')
        --force-rm                Always remove intermediate containers
        --iidfile string          Write the image ID to the file
        --isolation string        Container isolation technology
        --label list              Set metadata for an image
    -m, --memory bytes            Memory limit
        --memory-swap bytes       Swap limit equal to memory plus swap: '-1' to enable unlimited swap
        --network string          Set the networking mode for the RUN instructions during build (default "default")
        --no-cache                Do not use cache when building the image
        --pull                    Always attempt to pull a newer version of the image
    -q, --quiet                   Suppress the build output and print image ID on success
        --rm                      Remove intermediate containers after a successful build (default true)
        --security-opt strings    Security options
        --shm-size bytes          Size of /dev/shm
    -t, --tag list                Name and optionally a tag in the 'name:tag' format
        --target string           Set the target build stage to build.
        --ulimit ulimit           Ulimit options (default [])
    </pre>

- `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`
  Create a new image from a container's changes.

  Options:

    <pre>
    -a, --author string    Author (e.g., "John Hannibal Smith <hannibal@a-team.com>")
    -c, --change list      Apply Dockerfile instruction to the created image
    -m, --message string   Commit message
    -p, --pause            Pause container during commit (default true)
    </pre>
