SSH
===

* Adding `ControlPersist` to `~/.ssh/config` makes control sockets
  usable by leaving the socket around for a period if you close the
  last terminal session.  Prevents other sessions from then hanging.

```
ControlPath /tmp/%r@%h:%p
ControlMaster auto
ControlPersist 10m
```

Docker
======
* Restore init in Ubuntu base Docker images so upstart and such runs

```
FROM ubuntu:12.04
RUN rm /usr/sbin/policy-rc.d; \
    rm /sbin/initctl; dpkg-divert --rename --remove /sbin/initctl
```

* Remove all exited Docker containers

```
docker ps -a | grep Exit | cut -d ' ' -f 1 | xargs docker rm
```

Linux
=====

* Use prlimit to change ulimits on the fly

```
prlimit --pid $(pidof mecached) --nofile=8192:8192
```

Git
===

* Delete all local branches which have been merged into master

```
git branch --merged master | grep -v "\* master" | xargs -n 1 git branch -d
```

* Sign all commits
```
git config --global commit.gpgsign true
```

Command line
===============

* urldecode single url from commandline

```
echo $URL | python -c "import sys, urllib as ul; print ul.unquote_plus(sys.argv[1])"

```

* urldecode list of urls from the commandline

```
cat urls | python -c "import sys, urllib as ul; [sys.stdout.write(ul.quote_plus(l)) for l in sys.stdin]"
```

Shell
=====

* Log everything in a script to both console and syslog

```
exec 1> >(tee -ai /dev/console | logger -s -t $(basename $0)) 2>&1
```
