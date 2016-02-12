* Adding `ControlPersist` to `~/.ssh/config` makes control sockets
  usable by leaving the socket around for a period if you close the
  last terminal session.  Prevents other sessions from then hanging.

```
ControlPath /tmp/%r@%h:%p
ControlMaster auto
ControlPersist 10m
```

* Restore init in Ubuntu base Docker images so upstart and such runs

```
FROM ubuntu:12.04
RUN rm /usr/sbin/policy-rc.d; \
    rm /sbin/initctl; dpkg-divert --rename --remove /sbin/initctl
```
