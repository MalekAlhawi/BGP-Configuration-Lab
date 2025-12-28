
```cisco
hostname R1
! Site-A Router - BGP endpoint for LAN 192.168.10.0/24
! Connects to Site-C (hub)

!===============================
! BGP Configuration
!===============================
router bgp 20
 bgp router-id 1.1.1.1
 bgp log-neighbor-changes
 no synchronization
 neighbor 203.0.113.1 remote-as 35
 ! eBGP peer with Site-C
 network 192.168.10.0 mask 255.255.255.0
 ! Advertise Site-A LAN
 network 203.0.113.0 mask 255.255.255.252
 ! Advertise WAN subnet to Site-C

!===============================
! Interface Configuration
!===============================
interface GigabitEthernet0/0
 ip address 203.0.113.2 255.255.255.252
 duplex auto
 speed auto
 ! WAN interface to Site-C

interface GigabitEthernet0/1
 ip address 192.168.10.1 255.255.255.0
 duplex auto
 speed auto
 ! LAN interface

interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown
 ! Unused interface

interface Vlan1
 no ip address
 shutdown
 ! Default VLAN not used
