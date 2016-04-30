# Docker provider

### Installation

See [Installation instructions](Installation.md#docker-provider).

### Basic usage

```bash
vagrant status
vagrant up --provider=docker docker-kali
```

You can also export `VAGRANT_DEFAULT_PROVIDER` envvar if you plan to use vagrant only with docker:
```bash
export VAGRANT_DEFAULT_PROVIDER=docker
```

then:
```bash
vagrant up docker-kali
```

### Building vagrant into docker (Experimental!)

If you don't have vagrant, you can build pentest-env/vagrant container.
It needs the same client version as your host (cf DOCKER_VERSION in dockerfiles/vagrant)
```bash
docker build --no-cache -t pentest-env/vagrant -f dockerfiles/vagrant .
```

Make a magic alias (need docker permissions, or use `sudo`):

Without SELinux
```bash
alias vagrant="docker run --rm --name vagrant -it -v \"/var/run/docker.sock:/var/run/docker.sock\" -v \"\$(pwd):/vagrant\" pentest-env/vagrant"
```

With SELinux
```bash
alias vagrant="docker run --rm --name vagrant -it -v \"/var/run/docker.sock:/var/run/docker.sock:Z\" -v \"\$(pwd):/vagrant:Z\" pentest-env/vagrant"
```

### Known Issues

#### Vagrant-docker with SELinux

Check if docker can access docker host with :
```bash
docker run --rm --name vagrant -it -v "/var/run/docker.sock:/var/run/docker.sock:Z" -v "$(pwd):/vagrant:Z" --entrypoint docker pentest-env/vagrant info
```

```
setroubleshoot[17088]: failed to retrieve rpm info for /run/docker.sock
setroubleshoot[17088]: SELinux is preventing docker from connectto access on the unix_stream_socket /run/docker.sock. For complete SELinux messages. run sealert -l a12391c7-9f69-43d3-8127-1aedf6cac467
python3[17088]: SELinux is preventing docker from connectto access on the unix_stream_socket /run/docker.sock.

                                                              *****  Plugin catchall (100. confidence) suggests   **************************

                                                              If you believe that docker should be allowed connectto access on the docker.sock unix_stream_socket by default.
                                                              Then you should report this as a bug.
                                                              You can generate a local policy module to allow this access.
                                                              Do
                                                              allow this access for now by executing:
                                                              # ausearch -c docker --raw | audit2allow -M mypol
                                                              # semodule -i mypol.pp
```
