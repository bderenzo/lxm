# LXc container Manager

## Prerequisite

* Required: `lxc` package
* Optionnal: `iptables`, `iptables-persistent` and `lvm` packages

## Setup

To install lxm, with root rights:

* Clone the repo and go into it
* Run `./install`
* Configure the configuration file `/etc/lxm/lxm.conf`

If you want to use the integrated firewall (based on iptables):

* Run `fw init; fw test` and answer `y`

**Note**: If you lose access, rules are reset after 5 seconds without validation

## Usage

### Test installation

To test the installation, run `lxm version`

```
lxm 1.0.5, lxc 3.0.3
The MIT License: <https://mit-license.org>
Written by Baptiste DE RENZO
```

### Build container

To build a container:

* Create the data structure: `lxm init helloworld --bare`
* Go to container directory: `cd helloworld`
* Edit and complete the configuration file `ct.conf`, view [container build configuration](docs/container-build-config.md)
* Build container: `lxm build ct.conf`

### Manage container

* List container: `lxm ls`
* Get container info: `lxm info <name>`
* Execute a command in container: `lxm exec <name> <cmd>`
* Stop container: `lxm stop <name>`
* Delete container: `lxm rm <name>`
* Start all container: `lxm start all`
* Get a shell in container: `lxm go <name>`
* ...

## Help

To view the help, run `lxm help`

```
Available COMMANDS:

  init     NAME --bare          init a build data structure directories and files
  init     NAME [OPTS]          create a named container using the download template
  build    CONFIG [-f]          create container from configuration file
  rm       NAME [-y] [-f]       delete the named container
  start    NAME [NAME...]       start the named container(s)
  stop     NAME [NAME...]       stop the named container(s)
  restart  NAME [NAME...]       stop & start the named container(s)
  update   NAME [NAME...]       update the named running container(s)
  backup   NAME PATH            backup the named container
  restore  BACKUP NAME          restore the named container
  clone    NAME [CLONE]         clone the named container [to clone]
  attach   NAME                 attach the named container using bash as a default shell
  go       NAME                 start if not ready, and attach to the named container
  exec     NAME COMMAND         run a command on the named running container
  execfile NAME FILE            run a script on the named running container (with sh)
  ls       [PATTERN]            list of available containers [matching pattern]
  lsi      [PATTERN]            list of available images [matching pattern]
  cpumap   [PATTERN]            list of used cores [matchin pattern]
  info     NAME                 give information about the named container
  top      [NAME]               give top information about [named] container
  push     NAME SRC [DST]       copy the source file to the target path in the named container
  share    NAME SRC MNT [ro|rw] mount a shared directory on the named container
  unshare  NAME SRC             unmount the shared directory on the named container
  config   edit|set|get NAME    modify configuration of the named container
  help     [COMMAND]            displays help message [for the designated command]
  version                       show version
```

To view the detailed help of a command , run `lxm help command`

## Uninstall 

Just run, with root rights `./install --remove`

