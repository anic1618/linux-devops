# Devops in Proxy Setting
http_proxy=10.1.1.1:3122

https_proxy=10.1.1.2:3122

### Add in .bashrc (user) OR /etc/environment (all users)
```bash
    export http_proxy=proxyserver's ip:port
    export https_proxy=proxyserver's ip:port
    export NO_PROXY=localhost,127.0.0.1,master-node-ip, worker-node-ip etc      
```
### For docker 
src: https://docs.docker.com/config/daemon/systemd/
```
vi /etc/systemd/system/docker.service.d/http-proxy.conf
```
add lines
```
[Service]
Environment="HTTP_PROXY=proxyserver's ip:port"
Environment="HTTPS_PROXY=proxyserver's ip:port"
Environment="NO_PROXY=localhost,127.0.0.1,master-node-ip, worker-node-ip "
```
run cmd
```
  sudo systemctl daemon-reload
  sudo systemctl restart docker
```
See changes
```
  sudo systemctl show --property=Environment docker`

```
### Docker build and Docker Compose 
src:  https://docs.docker.com/config/daemon/systemd/#httphttps-proxy
```
vi ~/.docker/config.json with the following contents (replace proxy.server and port):
{
 "proxies":
 {
   "default":
   {
     "httpProxy": "http://proxy.server:port",
     "httpsProxy": "http://proxy.server:port",
     "noProxy": "localhost,127.0.0.1"
   }
 }
}
```
### APT 
``` 
cd /etc/apt/apt.conf.d
vi proxy_test
Acquire::http::Proxy "http://proxyserver's ip:port";
Acquire::https::Proxy "https://proxyserver's ip:port";
```
### GITHUB 
src: https://gist.github.com/evantoli/f8c23a37eb3558ab8765
```
SETUP
git config --global http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port
git config --global --get-regexp http.*

UNSET
git config --global --unset http.proxy
```

You can configure these globally in your user ~/.gitconfig file using the --global switch, or local to a repository in its .git/config file.

