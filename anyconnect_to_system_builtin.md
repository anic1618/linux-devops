## Convert Anyconnect to linux buildin network manager
### install anyconnect vpn client in network manager
sudo apt-get install openconnect network-manager-openconnect-gnome

### To configure the VPN using the Network Manager:

Click on the "Network Manager" icon in your System Tray on your desktop.
In the menu that appears, go to  VPN Connections -> Configure VPN
Click Add.
Choose Cisco AnyConnect Compatible VPN (openconnect) and click Create.
Enter the following information:
Connection name: Tech Services VPN
### convert usercertificate in .pfx to .pem
openssl pkcs12 -in certificatename.pfx -out certificatename.pem
### place above under User Certificate
### CA Certificate (vpnca-root.crt) 
convert cer to crt
### gateway as given
save
