## Important Tips

* Make sure the device and your Mac are on the **same network**.
* If there’s a firewall, make sure port **22** is open.
* If you're planning to SSH often, consider setting up **SSH key authentication** instead of using a password.


## MacOS Debugging (in my experience the dongle seems to be point of failure)

1. check firewall
   `sudo pfctl -d`
2. see connection 
   `sudo tcpdump -i en8 icmp`
3. ping 192.168.1.2
4. set mac address to switch and reset the ping so its not in memory
   `sudo arp -s 192.168.1.2 d8:b1:22:88:ad:ab`
5. networksetup -listallhardwareports
6. ifconfig enX
   - replace x with whatever port it is.


## Order of Operation

1. delete chassis auto-image-upgrade
2. set system services ssh root-login allow
3. set system root-authentication plain-text-password 
4. set interfaces <interface_name> unit 0 family inet address <XXX.XXX.X.X/Ports>
5. set routing-options static route 0.0.0.0/0 next-hop <hopAddress>

