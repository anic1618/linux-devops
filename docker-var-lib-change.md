### Steps to change Docker root as per Docker version 23.0.0
All with sudo 
#### Before downntime 
   1. Take a backup of docker.service file.
      
      $ cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.orig && cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.change

   2. Modify /lib/systemd/system/docker.service.change to tell docker to use our own directory 
      instead of default /var/lib/docker. In this example, I am using /p/var/lib/docker
      
      Apply below patch.
   
      ExecStart=/usr/bin/dockerd -g /p/var/lib/docker -H unix://
   
   3. mkdir -p /p/var/lib/docker/

   4. rsync existing docker data to our new location   

      $ rsync -aqxP /var/lib/docker/ /p/var/lib/docker/
      
###### scripts:

```bash
VAR_LIB=/p/var/lib/docker/
mkdir -p $VAR_LIB && cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.orig && cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.change && rsync -aqxP /var/lib/docker/  $VAR_LIB && cat << EOF
Modify /lib/systemd/system/docker.service.change to tell docker to use our own directory instead of default /var/lib/docker. In this example, I am using /p/var/lib/docker

Apply below patch.

ExecStart=/usr/bin/dockerd -g /p/var/lib/docker -H unix://
EOF   
```

#### Start Downtime   

   4. Stop docker service

      $ systemctl stop docker
   
   6. Do daemon-reload as we changed docker.service file   

      $ systemctl daemon-reload
   
   8. Start docker service   

      $ systemctl start docker

###### scripts after applying patch
```bash
mv /lib/systemd/system/docker.service.change /lib/systemd/system/docker.service  && systemctl stop docker && systemctl daemon-reload && systemctl stop docker
```
