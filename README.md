# DNS

Basic DNS Notes Repository
---

Notes about settings and tuning used in the DNS topic.

## DNS Installation

### Updating OS

```
# dnf clean all && dnf update
```

### Installing bind and tools

```
# dnf install bind bind-utils 
```

### Configure NTP (chrony)

```
# systemctl enable --now chronyd

# timedatectl set-timezone America/Mexico_City
```

### Setting up the DNS

- Backing up the default configuration

```
# tar czvf etc.named.bkp.tar.gz /etc/named*

# tar czvf var.named.bkp.tar.gz /var/named
```

- Delete the default configuration files

```
# rm -rf /etc/named* /etc/rndc* /var/named/*
```

- Create the master zone working directory

```
# mkdir -p /var/named/zones/master
```

- Label the master work directory for SELinux

```
# semanage fcontext -a -e /var/named /var/named/zones

# chcon --reference /var/named '/var/named/zones(/.*)?'

# restorecon -vR /var/named/zones
```

### DNS Config Files

- [Master](https://github.com/CursoIntegralLinux/dns/tree/main/master)
