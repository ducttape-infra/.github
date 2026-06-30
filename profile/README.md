[Ducttape infra tools](https://ducttape-infra.github.io)
====================

![](https://avatars.githubusercontent.com/u/296723703?s=140&v=4)

Like Dockerfiles, ducttape infra tools describe how to customize a base cloud image, installing packages, configuring services, and enabling systemd units, producing a reusable virtual machine images. Machinefiles are compatible with Podman and Dockerr Containerfiles, so you can create both containers and virtual machines from the same file! It is not meant to replace tools you have, but rather augment, such as Lima. This is also not replacing bootc, but rather provides you with a similar experience to prepare cloud-init based-images using Containerfiles, but still use a mutable Virtual Machine, ideal for experimentation. 



### [Ducttape](https://github.com/ducttape-infra/ducttape)

[![status-badge](https://ci.codeberg.org/api/badges/17521/status.svg)](https://ci.codeberg.org/repos/17521)

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

[![status-badge](https://ci.codeberg.org/api/badges/17522/status.svg)](https://ci.codeberg.org/repos/17522)

A lightweight execution engine designed to parse and execute Dockerfile or Containerfile instructions directly on a host system. It bridges the gap between container-native configuration formats and traditional host-based automation by treating a host (local or remote) as the target "container."

```dockerfile
FROM fedora-cloud

RUN dnf install -y httpd && \
    dnf clean all && \
    systemctl enable httpd
```


### [Actionfile](https://github.com/ducttape-infra/actionfile)

[![status-badge](https://ci.codeberg.org/api/badges/17520/status.svg)](https://ci.codeberg.org/repos/17520)

An _Actionfile_ is a Markdown-based configuration file that describes a set of actions, scripts, or tasks for use in automation workflows, dotfile management, or application deployment. It is designed for human readability and machine parsing, combining documentation, configuration, and executable code blocks in one file.


### [Integration with Packer](https://github.com/ducttape-infra/packer-machinefile)

The packer-test repository is a technical demonstration and framework for generating virtual machine (VM) disk images using Packer and Machinefile. It implements a Container-to-VM pattern, where system configurations are defined in a shared format and applied to various base distributions during the image creation process


### [Tapewrap](https://github.com/ducttape-infra/tapewrap)

[![status-badge](https://ci.codeberg.org/api/badges/17519/status.svg)](https://ci.codeberg.org/repos/17519)

A cross-platform resource and configuration management tool, compatible with GNU `stow`.


### [GitHub Actions](https://github.com/ducttape-actions/)

There are now actions to setup and deal with

  - shared INI-configuration files from a repository/file
  - remove unwanted stuff from a runner
  - install codium server
  - install VScode as tunnel
  - setup virtualization (qemu+kvm)
  - setup container tools (skopeo, etc)
  - setup ansible
  - execute jupyter notebpok
  - enable remote desktop for Windows runner
  - install Tailscale using authkey
 
and many more.
