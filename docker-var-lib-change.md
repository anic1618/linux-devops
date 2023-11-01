### Steps to change Docker root as per Docker version 23.0.0
#### Before downntime
   1. Take a backup of docker.service file.
      
      $ cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.orig

   3. rsync existing docker data to our new location   

      $ rsync -aqxP /var/lib/docker/ /p/var/lib/docker/

###### scripts:

```bash
cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.orig && rsync -aqxP /var/lib/docker/  /p/var/lib/docker/
```

#### Start Downtime   
   3. Modify /lib/systemd/system/docker.service to tell docker to use our own directory 
      instead of default /var/lib/docker. In this example, I am using /p/var/lib/docker
      
      Apply below patch.
   
      ExecStart=/usr/bin/dockerd -g /p/var/lib/docker -H unix://
    
   4. Stop docker service

      $ systemctl stop docker
   
   6. Do daemon-reload as we changed docker.service file   

      $ systemctl daemon-reload
   
   8. Start docker service   

      $ systemctl start docker

###### scripts after applying patch
```bash
systemctl stop docker && systemctl daemon-reload && systemctl stop docker
```
