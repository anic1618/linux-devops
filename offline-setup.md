## Debian Pkgs
```
sudo apt-get --print-uris --yes install <package-name> | grep ^\' | cut -d\' -f2 > downloads.list
cat downloads.list | xargs wget
cat  download.list | xargs basename -a | xargs dpkg -i
```
