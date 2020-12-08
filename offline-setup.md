## Debian Pkgs
```
docker run -it --name devtest2 -v ~/myprojects/pkgs:/app --network=host ubuntu:18.04  bash

```
```
sudo apt-get --print-uris --yes install <package-name> | grep ^\' | cut -d\' -f2 > downloads.list
cat downloads.list | xargs wget
cat  download.list | xargs basename -a | xargs dpkg -i
```
