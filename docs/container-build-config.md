## Container building configuration

The container building file (default `ct.conf`) contains everything needed to create a container from distribution to network configuration

* [OS](#operating-system-and-release)
* [Hostname](#hostname)
* [Disk](#disk)
* [CPU](#cpu)
* [Memory](#memory)
* [Network](#network)
* [Firewall](#firewall)
* [Mount](#mount-points)
* [Boot](#boot-options)
* [Kickstart](#kickstart-script)
* [LXC options](#lxc-options)

##### OS and release

```
os: alpine
release: 3.12
```

This configures the OS and the release of the container  
All avalaible OS and release for your architecure can be listed by running: `lxm lsi`

##### Hostname


```
hostname: helloworld
```

This configures the hostname and the name of the container

##### Disk

```
disk: 1G
```

This configures the main disk size of the container (works only with LVM backend)  
Size expressed in B, use K for KiB, M for MiB, G for GiB, T to TiB

##### CPU

```
cpu.cores: 1
cpu.time: 10%
```

This configures the number of CPU of the container and the prioriy given to this container over ther others  
CPU cores used by container can be viewed by running: `lxm cpumap`

##### Memory

```
memory: 256M
```

This configures the memory of the container
The default config doesn't configure any swap  
Size expressed in B, use K for KiB, M for MiB, G for GiB, T to TiB

##### Network

```
ip: 10.10.10.5
```

This configures a static ip adress for the container  
Gateway, Netmask, DNS, etc. are globally configured in `/etc/lxm/lxm.conf`  
**Note:** Currently only works for debian or alpine container

##### Firewall

```
fw.in: 22/tcp
fw.out: 53/udp,80/tcp,443/tcp
fw.log: false
```

If enabled in `/etc/lxm/lxm.conf`, this configures hypervisor firewall (input and output) rules and logs for the container. Logs can be viewed in hypervisor kernel log file

Rules are either a comma separated list of ports, `all` to accept everything or `none` to reject everything  
Ports are suffixed by `/tcp`, `/udp` or nothing for both  
Default is destination port (example `80/tcp`). `s` prefixed number is for source port (example `s53000/tcp`)

##### Mount points

```
mp.0: ./data:/data
mp.1: /mnt/disk/static:/static:ro
```

This configures hypervisor disk shared to container  
The first path is hypervisor path (absolute or relative to config file), the second the container mount point  
Optionally `:ro` can be added for a readonly disk in container

##### Boot options

```
start.auto: 1
start.order: 8
start.delay: 10
```

This configures the container auto-start, order and delay on hypervisor reboot

##### Kickstart script

```
ks.0: ./scripts/install.sh
ks.1: ./scripts/configure.sh
```

This configure scripts executed in container  
The path corresponds to script location on hypervisor. Script is copied to container (in /tmp) then executed  
It is usefull to install binaries or configure applications

##### LXC options

```
lxc.cgroup.devices.allow = c 10:200 rwm
lxc.hook.autodev = sh -c "cd ${LXC_ROOTFS_MOUNT}/dev && mkdir net && mknod -m 666 net/tun c 10 200"
```

Options starting with `lxc.` are append to container configuration  
**Warning**: these options and their values are separated by an equal `=` sign and not a colon `:`

