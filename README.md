* Adding `ControlPersist` to `~/.ssh/config` makes control sockets
  usable by leaving the socket around for a period if you close the
  last terminal session.  Prevents other sessions from then hanging.

```
ControlPath /tmp/%r@%h:%p
ControlMaster auto
ControlPersist 10m
```
