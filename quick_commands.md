# Documentation on Interacting with JUNOS CLI
1. This documentation assumes you are interacting with HPE-Juniper routers
2. I skip explaining why you would need commands (e.g. scenarios)
3. This document is intended to be a quick reference for commands that you should know like the back of your hand and understand why you need to run these commands
4. You typically automate these commands for enterprise set ups 

## Graceful Shutdown Then Unplug power
request system power-off

- this halts the switch, if you press a button it can reboot it and if you unplug it will kill the machine
- a bad shutdown can corrupt data

## Connecting to device with minicom
sudo minicom -D /dev/tty.usbserial-A951NCCW -b 9600
- understand your switches/routers baud rate frequency it needs

## Displaying devices 
ls -l /dev/* 

- This will display all devices, find your device serial number

## Config Interfaces
show configuration interfaces

<details>

```json

ge-0/0/0 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/1 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/2 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/3 {
    unit 0 {
        family ethernet-switching {     
            storm-control default;      
        }
    }
}
ge-0/0/4 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/5 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/6 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }                                   
}
ge-0/0/7 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/8 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/9 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/10 {                             
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/0/11 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
ge-0/1/0 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
xe-0/1/0 {
    unit 0 {
        family ethernet-switching {     
            storm-control default;
        }
    }
}
ge-0/1/1 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
xe-0/1/1 {
    unit 0 {
        family ethernet-switching {
            storm-control default;
        }
    }
}
irb {
    unit 0 {
        family inet;
        family inet6;
    }                                   
}
vme {
    unit 0 {
        family inet;
        family inet6;
    }
}
```

</details>

## See SSH and Telnet
show configuration system services 

```
netconf {
    ssh;
    rfc-compliant;
    yang-compliant;
}
ssh {
    connection-limit 10;
}
telnet {
    connection-limit 10;
}

```

## Display config settings related to connection
show configuration system services


## Display the hostname set by user
show configuration system host-name

## Routing
show configuration routing-options

## Enter edit mode
configure

## Enter cli 
cli 

## Set MGMT Interface
set interfaces <interface_name> unit 0 family inet address <XXX.XXX.X.X/Ports>
- IPv4 address
- Subnet Mask
- Sets the IP address used to manage the switch remotely over the network

## Static route
set routing-options static route 0.0.0.0/0 next-hop <hopAddress>
- The static route ensures the provider network can route to all remote destinations in the customer network by forwarding traffic through the customer device.

## Allow Root Login over ssh
set system services ssh root-login allow 
set system root-authentication plain-text-password 

## You cant have me0 and vme running at same time
set interfaces me0 unit 0 family inet address <ip/port>

## Show interfaces up 
show interfaces terse
show interfaces me0 terse 
show interfaces terse | match "me0|vme" 
show interfaces me0 detail # or show interfaces me0 extensive 
<details>
    ```
            Physical interface: me0, Enabled, Physical link is Up
        Interface index: 64, SNMP ifIndex: 33, Generation: 1
        Type: Ethernet, Link-level type: Ethernet, MTU: 1514, Clocking: Unspecified,
        Speed: 100mbps
        Device flags   : Present Running
        Interface flags: SNMP-Traps
        Link type      : Full-Duplex
        Link flags     : 0x4
        Physical info  : Unspecified
        Hold-times     : Up 0 ms, Down 0 ms
        Current address: <macaddress>, Hardware address: <macaddress>
        Alternate link address: Unspecified
        Last flapped   : 2025-05-17 14:03:59 UTC (00:00:53 ago)
        Statistics last cleared: Never
        Traffic statistics:
        Input  bytes  :               217952
        Output bytes  :                21327
        Input  packets:                  521
        Output packets:                  174
        IPv6 transit statistics:
        Input  bytes  :                    0
        Output bytes  :                    0
        Input  packets:                    0
        Output packets:                    0 

        Logical interface me0.0 (Index 7) (SNMP ifIndex 34) (Generation 5)
            Flags: Up SNMP-Traps 0x4000000 Encapsulation: ENET2
            Traffic statistics:
            Input  bytes  :                87602
            Output bytes  :                 6651
            Input  packets:                  202
            Output packets:                   51
        Local statistics:
            Input  bytes  :                87602
            Output bytes  :                 6651
            Input  packets:                  202
            Output packets:                   51
            Protocol inet, MTU: 1500
            Max nh cache: 75000, New hold nh limit: 75000, Curr nh cnt: 1,
            Curr new hold cnt: 1, NH drop cnt: 0
            Generation: 178, Route table: 0
            Flags: Sendbcast-pkt-to-re
            Addresses, Flags: Is-Default Is-Preferred Is-Primary
                Destination: <ip/ports>, Local: <ip>, Broadcast: <broadcastIP>,
                Generation: 7
        ```
</details>
show configuration interfaces me0 
show configuration firewall
show configuration security

## Address Resolution Protocol
- no-resolve indicates you don't want to do DNS lookups for every IP address in the ARP table

show arp no-resolve | match <address>


## Delete interfaces
delete interfaces

## When you make error
rollback 0

## Creating super user
set system login user <username> class super-user authentication plain-text-password

## Debugging why SSH is not working on local device

1. Delete interface, and use AP family (left most AP connection ethernet connection instead of mangement port for connection)
delete interfaces me0 
delete interfaces ge-0/0/0

<details>
```bash
Possible completions:
  <[Enter]>            Execute this command
> accept-source-mac    Remote media access control address to/from which to accept traffic
  accounting-profile   Accounting profile name
  alias                Interface alias
+ apply-groups         Groups from which to inherit configuration data
+ apply-groups-except  Don't inherit configuration data from these groups
> arp-resp             Knob to control ARP response on the interface, default is restricted
  bandwidth            Logical unit bandwidth (informational only)
  description          Text description of interface
  disable              Disable this logical interface
  encapsulation        Logical link-layer encapsulation
  etree-ac-role        ETREE attachment circuit role
> family               Protocol family
  generate-eui64       To generate Link Local EUI-64 addresses
+ inner-vlan-id-swap-ranges  Inner vlan-id swap range(s) of form vid1-vid2 for dynamic L2 VLANs
> input-vlan-map       VLAN map operation on input
> interface-shared-with  Specify which PSD owns this logical interface
  interface-tag        Interface tag name
  no-generate-eui64    Don't to generate Link Local EUI-64 addresses
```
</details>
set interfaces ge-0/0/0.0 family inet address <ip/port> 

2. Allow ssh
set system services ssh root-login allow

3. Commit, but with rollback of 10 minutes
commit confirmed 10
*commit confirmed will be automatically rolled back in 10 minutes unless confirmed*

4. Try pinging address then run below command

5. run show interfaces terse | except down 