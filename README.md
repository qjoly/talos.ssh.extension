# Talos.SSH.Extension

This repository contains the Talos SSH Extension, which provides SSH access to Talos nodes. This is only useful for development/debugging purposes, as Talos is designed to be managed through its API and CLI tools.

Be careful to not use this in any production environment, as it will expose SSH access to your Talos nodes, which is very dangerous. Plus, I voluntarily added a mountpoint to access system files (remember, debugging only).

## Features

Well, since I used the [LinuxServer.io base image](https://github.com/linuxserver/docker-openssh-server), it has all the features of that project, you can find them [here](https://github.com/linuxserver/docker-openssh-server).

:warning: I insist on the fact you have to read the LinuxServer.io documentation, there are some important things you have to know about the SSH server configuration, like the fact that removing a key in the environment variables will not remove it from the authorized_keys file.

## Usage

You have to upgrade (or install nodes) with the `ssh` extension enabled. You can do this by using the `talosctl upgrade` command or by setting a custom installer image in the machine configuration (`.machine.install.image`).

```bash
talosctl upgrade -i ghcr.io/qjoly/talos.ssh.extension/installer:v1.10.5-amd64
```

Get the logs of the ssh daemon:
```bash
talosctl logs ext-ssh
```

Once installed, you can now to inject configuration into the nodes by patching the machine configuration. You can do this by using the `talosctl patch` command.

```yaml
# Example Extension configuration
apiVersion: v1alpha1
kind: ExtensionServiceConfig
name: ssh
environment:
  - PUBLIC_KEY=mybeautifulpublickey
  - PUBLIC_KEY_URL=https://github.com/qjoly.keys
``` 

```bash
talosctl patch mc -p @talos.ssh.extension.patch.yaml
```


