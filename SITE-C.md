```cisco
hostname R3
! Site-C Router - Hub connecting Site-A and Site-B
! Handles eBGP peering with both sites

!===============================
! BGP Configuration
!===============================
router bgp 35
 bgp router-id 3.3.3.3
 bgp log-neighbor-changes
 no synchronization
 neighbor 203.0.113.2 remote-as 20
 ! eBGP peer with Site-A
 neighbor 192.0.2.2 remote-as 50
 ! eBGP peer with Site-B
 network 203.0.113.0 mask 255.255.255.252
 ! Advertise WAN subnet to Site-A
 network 192.0.2.0 mask 255.255.255.252
 ! Advertise WAN subnet to Site-B

!===============================
! Interface Configuration
!===============================
interface GigabitEthernet0/0
 ip address 203.0.113.1 255.255.255.252
 duplex auto
 speed auto
 ! WAN interface to Site-A

interface GigabitEthernet0/1
 ip address 192.0.2.1 255.255.255.252
 duplex auto
 speed auto
 ! WAN interface to Site-B

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
