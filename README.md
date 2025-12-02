    Router>
    Router>enable
    Router#
    Router#configure terminal
    Enter configuration commands, one per line.  End with CNTL/Z.
    Router(config)#
    Router(config)#hostname R4
    R4(config)#
    R4(config)#enable secret CCNA
    R4(config)#
    R4(config)#interface loopback0
    
    R4(config-if)#
    %LINK-3-UPDOWN: Interface Loopback0, changed state to down
    
    %LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback0, changed state to up
    
    R4(config-if)#ip address 4.4.4.4 255.255.255.255
    R4(config-if)#
    R4(config-if)#interface g0/0/0
    R4(config-if)#
    R4(config-if)#ip address 192.168.1.62 255.255.255.252
    R4(config-if)#
    R4(config-if)#no shutdown
    
    R4(config-if)#
    %LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
    
    %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
    
    R4(config-if)#do show controllers interface s0/1/0
    show controllers interface s0/1/0
                     ^
    % Invalid input detected at '^' marker.
    	
    R4(config-if)#do show controllers s0/1/0
    Interface Serial0/1/0
    Hardware is PowerQUICC MPC860
    DCE V.35, clock rate 2000000
    idb at 0x81081AC4, driver data structure at 0x81084AC0
    SCC Registers:
    General [GSMR]=0x2:0x00000000, Protocol-specific [PSMR]=0x8
    Events [SCCE]=0x0000, Mask [SCCM]=0x0000, Status [SCCS]=0x00
    Transmit on Demand [TODR]=0x0, Data Sync [DSR]=0x7E7E
    Interrupt Registers:
    Config [CICR]=0x00367F80, Pending [CIPR]=0x0000C000
    Mask   [CIMR]=0x00200000, In-srv  [CISR]=0x00000000
    Command register [CR]=0x580
    Port A [PADIR]=0x1030, [PAPAR]=0xFFFF
           [PAODR]=0x0010, [PADAT]=0xCBFF
    Port B [PBDIR]=0x09C0F, [PBPAR]=0x0800E
           [PBODR]=0x00000, [PBDAT]=0x3FFFD
    Port C [PCDIR]=0x00C, [PCPAR]=0x200
           [PCSO]=0xC20,  [PCDAT]=0xDF2, [PCINT]=0x00F
    Receive Ring
            rmd(68012830): status 9000 length 60C address 3B6DAC4
            rmd(68012838): status B000 length 60C address 3B6D444
    Transmit Ring
    
    R4(config-if)#
    R4(config-if)#interface s0/1/0
    R4(config-if)#
    R4(config-if)#clock rate 2000000
    R4(config-if)#
    R4(config-if)#ip address 192.168.1.58 255.255.255.252
    R4(config-if)#
    R4(config-if)#no shutdown
    
    R4(config-if)#
    %LINK-5-CHANGED: Interface Serial0/1/0, changed state to up
    
    R4(config-if)#
    %LINEPROTO-5-UPDOWN: Line protocol on Interface Serial0/1/0, changed state to up
    
    R4(config-if)#
    R4(config-if)#do show ip interface brief
    Interface              IP-Address      OK? Method Status                Protocol 
    GigabitEthernet0/0/0   192.168.1.62    YES manual up                    up 
    GigabitEthernet0/0/1   unassigned      YES unset  administratively down down 
    GigabitEthernet0/0/2   unassigned      YES unset  administratively down down 
    Serial0/1/0            192.168.1.58    YES manual up                    up 
    Serial0/1/1            unassigned      YES unset  administratively down down 
    Loopback0              4.4.4.4         YES manual up                    up 
    Vlan1                  unassigned      YES unset  administratively down down
    R4(config-if)#
    R4(config-if)#
    R4(config-if)#interface g0/0/1
    R4(config-if)#
    R4(config-if)#ip address 200.168.1.21 255.255.255.252
    R4(config-if)#
    R4(config-if)#no shutdown
    
    R4(config-if)#
    %LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up
    
    R4(config-if)#exit
    R4(config)#
    R4(config)#router eigrp 1
    R4(config-router)#
    R4(config-router)#no auto-summary
    R4(config-router)#
    R4(config-router)#passive-interface g0/0/1
    R4(config-router)#
    R4(config-router)#network 192.168.1.0
    R4(config-router)#
    %DUAL-5-NBRCHANGE: IP-EIGRP 1: Neighbor 192.168.1.57 (Serial0/1/0) is up: new adjacency
    R4(config-router)#
    R4(config-router)#variance 2
    R4(config-router)#
    %DUAL-5-NBRCHANGE: IP-EIGRP 1: Neighbor 192.168.1.61 (GigabitEthernet0/0/0) is up: new adjacency
    
    %DUAL-5-NBRCHANGE: IP-EIGRP 1: Neighbor 192.168.1.57 (Serial0/1/0) is up: new adjacency
    R4(config-router)#do write
    Building configuration...
    [OK]
    R4(config-router)#exit
    R4(config)#
    R4(config)#ip route 0.0.0.0 0.0.0.0 200.168.1.22
    R4(config)#
    R4(config)#do show ip route
    Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
           D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
           N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
           E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
           i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
           * - candidate default, U - per-user static route, o - ODR
           P - periodic downloaded static route
    
    Gateway of last resort is 200.168.1.22 to network 0.0.0.0
    
         4.0.0.0/32 is subnetted, 1 subnets
    C       4.4.4.4/32 is directly connected, Loopback0
         192.168.1.0/24 is variably subnetted, 9 subnets, 3 masks
    D       192.168.1.0/28 [90/3072] via 192.168.1.61, 00:25:09, GigabitEthernet0/0/0
    D       192.168.1.16/28 [90/2170368] via 192.168.1.61, 00:08:29, GigabitEthernet0/0/0
                            [90/2170368] via 192.168.1.57, 00:08:28, Serial0/1/0
    D       192.168.1.32/28 [90/2170112] via 192.168.1.57, 00:44:04, Serial0/1/0
    D       192.168.1.48/30 [90/2170112] via 192.168.1.57, 00:44:04, Serial0/1/0
    D       192.168.1.52/30 [90/2170112] via 192.168.1.61, 00:25:09, GigabitEthernet0/0/0
    C       192.168.1.56/30 is directly connected, Serial0/1/0
    L       192.168.1.58/32 is directly connected, Serial0/1/0
    C       192.168.1.60/30 is directly connected, GigabitEthernet0/0/0
    L       192.168.1.62/32 is directly connected, GigabitEthernet0/0/0
         200.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
    C       200.168.1.20/30 is directly connected, GigabitEthernet0/0/1
    L       200.168.1.21/32 is directly connected, GigabitEthernet0/0/1
    S*   0.0.0.0/0 [1/0] via 200.168.1.22
    
    R4(config)#
    R4(config)#do show ip eigrp topology
    IP-EIGRP Topology Table for AS 1/ID(4.4.4.4)
    
    Codes: P - Passive, A - Active, U - Update, Q - Query, R - Reply,
           r - Reply status
    
    P 192.168.1.0/28, 1 successors, FD is 3072
             via 192.168.1.61 (3072/2816), GigabitEthernet0/0/0
    P 192.168.1.16/28, 2 successors, FD is 2170368
             via 192.168.1.61 (2170368/2170112), GigabitEthernet0/0/0
             via 192.168.1.57 (2170368/3072), Serial0/1/0
    P 192.168.1.32/28, 1 successors, FD is 2170112
             via 192.168.1.57 (2170112/2816), Serial0/1/0
    P 192.168.1.48/30, 1 successors, FD is 2170112
             via 192.168.1.57 (2170112/2816), Serial0/1/0
    P 192.168.1.52/30, 1 successors, FD is 2170112
             via 192.168.1.61 (2170112/2169856), GigabitEthernet0/0/0
    P 192.168.1.56/30, 1 successors, FD is 2169856
             via Connected, Serial0/1/0
    P 192.168.1.60/30, 1 successors, FD is 2816
             via Connected, GigabitEthernet0/0/0
    R4(config)#
    R4(config)#
