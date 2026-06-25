Ducttape infra tools
====================

### [Ducttape](https://github.com/ducttape-infra/ducttape)

Ducttape is a command-line tool designed to bridge the gap between container-like workflows and virtual machine (VM) management. It allows developers to build, run, and share VM images using a syntax and lifecycle similar to Docker or Podman, powered by the Machinefile format.

```sh
ducttape build -t my-httpd -f examples/Machinefile.httpd -d fedora-cloud
```

```sh
ducttape run my-httpd
```

```sh
ducttape shell my-httpd curl -s http://localhost/
```


### [Machinefile](https://github.com/ducttape-infra/Machinefile)

A lightweight execution engine designed to parse and execute Dockerfile or Containerfile instructions directly on a host system. It bridges the gap between container-native configuration formats and traditional host-based automation by treating a host (local or remote) as the target "container."

```dockerfile
FROM fedora-cloud

RUN dnf install -y httpd && \
    dnf clean all && \
    systemctl enable httpd
```
