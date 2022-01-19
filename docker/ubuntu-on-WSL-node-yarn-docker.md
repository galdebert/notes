
# check ubuntu version from the command-line

`lsb_release -a`

# install nodejs on ubuntu 20.04

https://linuxize.com/post/how-to-install-node-js-on-ubuntu-20-04/

- from standard Ubuntu repositories but it's nodejs 10.19.0

- From the NodeSource repository. Use this repository if you want to install a different Node.js version than the one provided in the Ubuntu repositories. Currently, NodeSource supports Node.js `v14.x`, `v13.x`, `v12.x`, and `v10.x`.

- Using nvm (Node Version Manager). This tool allows you to have **multiple Node.js versions installed on the same machine**. If you are Node.js developer, then this is the preferred way of installing Node.js.

https://github.com/nvm-sh/nvm

nvm is a version manager for node.js, designed to be installed per-user, and invoked per-shell. nvm works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash), in particular on these platforms: unix, macOS, and windows WSL.

INSTALL

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash`

Usage

To install a specific version of node: `nvm install 14.16.0`
To switch among installed versions:    `nvm use 14`
list available versions of node:       `nvm list-remote`


# install yarn on ubuntu 20.04

It is recommended to install Yarn through the npm package manager, which comes bundled with Node.js when you install it on your system.

Note this installs yarn classic (not yarn 2)

`npm install --global yarn`

# edit code in the WSL file system using vscode on windows

from the WSL ubuntu terminal:

`galdebert@DESKTOP-PTP0E6B:~/js-angusj-clipper$ code .`

note the **WSL: Ubuntu** green field on the lower left corner of vscode. It's the remote window.


# Docker for windows on WSL 2 - Docker installed on the WSL linux distribution

When we installed **Docker Desktop for windows 4.1.1** it installed docker **inside our WSL 2 linux distribution** !
We can check that easily :

in docker app > Settings > Resources
- You are using the WSL 2 backend, so resource limits are managed by Windows.
- WSL Integration Configure which WSL 2 distros you want to access Docker from.
  - Enable integration with my default WSL distro is CHECKED
  - 
in docker app > Settings > Docker Engine
- Docker Engine v20.10.8

also, from https://docs.docker.com/desktop/windows/wsl/#best-practices
> To avoid any potential conflicts with using WSL 2 on Docker Desktop, you must uninstall any previous versions of Docker Engine and CLI installed directly through Linux distributions before installing Docker Desktop.

# running yarn scripts from the WSL

from the vscode terminal, when we run

`galdebert@DESKTOP-PTP0E6B:~/js-angusj-clipper$ yarn build`,

it runs scripts fully in Linux and uses the Docker we installed with **Docker Desktop for windows**

```
galdebert@DESKTOP-PTP0E6B:~/js-angusj-clipper$ docker -v
Docker version 20.10.8, build 3967b7d
```
