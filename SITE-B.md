```cisco
hostname R2
! Site-B Router - BGP endpoint for LAN 192.168.20.0/24
! Connects to Site-C (hub)

!===============================
! BGP Configuration
!===============================
router bgp 50
 bgp router-id 2.2.2.2
 bgp log-neighbor-changes
 no synchronization
 neighbor 192.0.2.1 remote-as 35
 ! eBGP peer with Site-C
 network 192.168.20.0 mask 255.255.255.0
 ! Advertise Site-B LAN
 network 192.0.2.0 mask 255.255.255.252
 ! Advertise WAN subnet to Site-C

!===============================
! Interface Configuration
!===============================
interface GigabitEthernet0/0
 ip address 192.0.2.2 255.255.255.252
 duplex auto
 speed auto
 ! WAN interface to Site-C

interface GigabitEthernet0/1
 ip address 192.168.20.1 255.255.255.0
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
