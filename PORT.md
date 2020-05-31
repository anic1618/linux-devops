### Run netstat command along with grep command to filter out port in LISTEN state:
netstat -tulpn | grep LISTEN

#### OR

sudo ss -tulw
sudo ss -tulwn

-t : Show only TCP sockets on Linux

-u : Display only UDP sockets on Linux

-l : Show listening sockets. For example, TCP port 22 is opened by SSHD server.

-p : List process name that opened sockets

-n : Don’t resolve service names i.e. don’t use DNS


