### Steps to change Docker root as per Docker version 23.0.0
All with sudo 
#### Before downntime 
   1. Take a backup of docker.service file.
      
      $ cp /etc/docker/daemon.json /etc/docker/daemon.json.orig 
      
   
   2. mkdir -p /p/var/lib/docker/

   3. rsync existing docker data to our new location   

      $ rsync -aqxP /var/lib/docker/ /p/var/lib/docker/

   4. edit /etc/docker/daemon.json
      {
       "data-root": " /p/var/lib/docker/"
      }
      


#### Start Downtime   

   5. daemon-reload as we changed docker.service file   

      $ systemctl daemon-reload
   
   6. Start docker service   

      $ systemctl restart docker
   
   7.Validate the new Docker root location:
      docker info -f '{{ .DockerRootDir}}'

source: https://www.ibm.com/docs/en/z-logdata-analytics/5.1.0?topic=compose-relocating-docker-root-directory


