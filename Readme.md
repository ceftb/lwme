# Lightweight Materialization Environment

This is a very light-weight docker-composed based materialization environment for ceftb1. The environment is composed of a 15 containers with names corresponding to the names in ceftb1. This can be used as a starting point for creating behavioral model tools. Feel free to modify the docker-compose script as needed to launch or own code (instead of sleeping). Below is a simple example of how to get going.

To start the environment

```
docker-compose up
```

This starts up a bunch of containers that are sleeping. In another shell

```
docker-compose ps
```

Should give something along the lines of 

```
       Name               Command        State   Ports
------------------------------------------------------
ceftb1dc_droid0_1    sleep infinity      Up
ceftb1dc_droid1_1    sleep infinity      Up
ceftb1dc_droid2_1    sleep infinity      Up
ceftb1dc_minnow0_1   sleep infinity      Up
ceftb1dc_minnow1_1   sleep infinity      Up
ceftb1dc_minnow2_1   sleep infinity      Up
ceftb1dc_netmu0_1    sleep infinity      Up
ceftb1dc_netmu1_1    sleep infinity      Up
ceftb1dc_netmu2_1    sleep infinity      Up
ceftb1dc_nodemu0_1   tail -f /dev/null   Up
ceftb1dc_nodemu1_1   tail -f /dev/null   Up
ceftb1dc_nodemu2_1   tail -f /dev/null   Up
ceftb1dc_rpi0_1      sleep infinity      Up
ceftb1dc_rpi1_1      sleep infinity      Up
ceftb1dc_rpi2_1      sleep infinity      Up
```


Now you can execute code in any of these containers like so

```
[ry@ryzen ceftb1-dc]$ docker-compose exec rpi1 /bin/bash
root@2de2cf70d926:/# ping droid2
PING droid2 (172.21.0.11): 56 data bytes
64 bytes from 172.21.0.11: icmp_seq=0 ttl=64 time=0.209 ms
64 bytes from 172.21.0.11: icmp_seq=1 ttl=64 time=0.100 ms
64 bytes from 172.21.0.11: icmp_seq=2 ttl=64 time=0.100 ms
^C--- droid2 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.100/0.136/0.209/0.051 ms
root@2de2cf70d926:/# 

```

Note that each container has name resolution of the others. The nodemu containers run busybox (a very lightweight linux distro) so you will need to use `/bin/ash` for those.

