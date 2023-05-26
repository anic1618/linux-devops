1. Take a backup of docker.service file.
   $ cp /lib/systemd/system/docker.service /lib/systemd/system/docker.service.orig

2. Modify /lib/systemd/system/docker.service to tell docker to use our own directory 
   instead of default /var/lib/docker. In this example, I am using /p/var/lib/docker
   
   Apply below patch.

   ExecStart=/usr/bin/dockerd -g /p/var/lib/docker -H unix://
 
3. Stop docker service
   $ systemctl stop docker
4. Do daemon-reload as we changed docker.service file   
   $ systemctl daemon-reload
5. rsync existing docker data to our new location   
   $ rsync -aqxP /var/lib/docker/ /p/var/lib/docker/
6. Start docker service   
   $ systemctl stop docker
