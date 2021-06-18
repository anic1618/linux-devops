This would 'disconnect' after 90 seconds of no response from the server, and then AutoSSH would reconnect automatically.
otherwise -M Port no should have the assigned port no on remote

autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -L 5000:localhost:3306 user@randomhost.org

https://www.everythingcli.org/ssh-tunnelling-for-fun-and-profit-autossh/

