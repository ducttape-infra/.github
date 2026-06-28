Ducttape infra tools
====================


Like Dockerfiles, ducttape infra tools describe how to customize a base cloud image, installing packages, configuring services, and enabling systemd units, producing a reusable virtual machine images. Machinefiles are compatible with Podman and Dockerr Containerfiles, so you can create both containers and virtual machines from the same file! It is not meant to replace tools you have, but rather augment, such as Lima. This is also not replacing bootc, but rather provides you with a similar experience to prepare cloud-init based-images using Containerfiles, but still use a mutable Virtual Machine, ideal for experimentation. 


### [Ducttape](https://github.com/ducttape-infra/ducttape)

Ducttape is a command-line tool designed to bridge the gap between container-like workflows and virtual machine (VM) management. It allows developers to build, run, and share VM images using a syntax and lifecycle similar to Docker or Podman, powered by the Machinefile format.

`Machinefile`
```Dockerfile
FROM fedora-cloud:44

RUN dnf install -y httpd && \
  dnf clean all && \
  systemctl enable httpd
```

```sh
ducttape build -t my-httpd -f Machinefile
```

```sh
ducttape run my-httpd --publish 8080:80
```

```sh
ducttape shell my-httpd curl -s http://localhost/
```

```sh
curl http://$(ducttape ports my-httpd :80)
```

### [Machinefile](https://github.com/ducttape-infra/Machinefile)

A lightweight execution engine designed to parse and execute Dockerfile or Containerfile instructions directly on a host system. It bridges the gap between container-native configuration formats and traditional host-based automation by treating a host (local or remote) as the target "container."

```dockerfile
FROM fedora-cloud

RUN dnf install -y httpd && \
    dnf clean all && \
    systemctl enable httpd
```

### [Actionfile](https://github.com/ducttape-infra/action.sh)

Runs scriptblocks from run Actionfiles, a Markdown-based configuration file that describes a set of actions, scripts, or tasks for use in automation workflows


### [Integration with Packer](https://github.com/ducttape-infra/packer-machinefile)

The packer-test repository is a technical demonstration and framework for generating virtual machine (VM) disk images using Packer and Machinefile. It implements a Container-to-VM pattern, where system configurations are defined in a shared format and applied to various base distributions during the image creation process
