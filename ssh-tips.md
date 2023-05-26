### remote SSH with a jump host
usecases: vscode

Configure ssh client: Open your .ssh/config file and add the following content
```
# We will set a 1 minute keep alive to keep the connection
# active if there is no activity to avoid unwanted disconnects
Host *
  ServerAliveInterval 60

# Specify our intermediate jump host, nothing fancy here
# we just tell what the host name is for now.
Host jump-host
  HostName myjumphost.domain.com

# Now we will specify the actual remote host with
# the jump host as the proxy. Specify remote hostname
# as the jump-host would see it since we will be connecting
# from the jump host.
Host remote-host
  HostName remote-host.domain.com
  ProxyCommand ssh -W %h:%p jump-host
```
