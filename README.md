# Junos Devices

- [Documentation](https://www.juniper.net/documentation/us/en/hardware/ex2300/topics/topic-map/connecting-ex2300-management-devices.html)
- [Routing Protocols and Commands](https://www.juniper.net/documentation/us/en/software/junos/static-routing/topics/topic-map/config_static-routes.html)

1. You need some sort of terminal emulators and serial communication programs to communicate with the router
    a. Securecrt allows you to organize your connections for faster automation 
2. Quick note when you first connect:
    - Amnesiac is unconfigured 
        a. It tries connecting to the internet, via DHCIP, to update the image. 
        b. Zero rise, you have to set the root password on full wipe, to set the configuration.
        c. Root password is just root and enter, and then set it. 
3. delete chassis auto-image-upgrade to get rid of annoying prompt
4. show chassis alarm 
    - configuration settings that you need to set
        	a. Ethernet link Is down 
            b. Management needs to be configured. 
            c. Mgmnt port to the mgnt network
5. Uplink next layer devices (wireless)

## Setting up a Mesh Network
- create redundancies for the serial ports and uplinks if one of them goes down. 
- Applies to both serial ports AND the access points if they go down
