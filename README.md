
# VLAN Configuration

## Addressing Table

| Device | Interface | IP Address    | Subnet Mask    | VLAN |
|--------|-----------|---------------|----------------|------|
| PC1    | NIC       | 172.17.10.21  | 255.255.255.0  | 10   |
| PC2    | NIC       | 172.17.20.22  | 255.255.255.0  | 20   |
| PC3    | NIC       | 172.17.30.23  | 255.255.255.0  | 30   |
| PC4    | NIC       | 172.17.10.24  | 255.255.255.0  | 10   |
| PC5    | NIC       | 172.17.20.25  | 255.255.255.0  | 20   |
| PC6    | NIC       | 172.17.30.26  | 255.255.255.0  | 30   |

<p align="center">
  <img src="https://github.com/user-attachments/assets/ae5702da-35bc-4e8b-a6a3-7ef556b81e0c" height="100%" width="100%" alt=""/>
  
</p>

## Objectives

1. Verify the Default VLAN Configuration
2. Configure VLANs
3. Assign VLANs to Ports

## Background

VLANs are beneficial in managing logical groups, allowing members to be easily moved, changed, or added. This activity focuses on creating and naming VLANs, and assigning access ports to specific VLANs.

## Part 1: Verify the Default VLAN Configuration

### Display the Current VLANs

On S1, I issue the command to display all VLANs configured. By default, all interfaces are assigned to VLAN 1.

```plaintext
S1# show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
```

### Verify Connectivity Between PCs on the Same Network

I verify that each PC can ping another PC on the same subnet:

- PC1 can ping PC4
- PC2 can ping PC5
- PC3 can ping PC6

Pings to hosts on other networks fail.

#### Question:

What benefits can VLANs provide to the network?

VLANs allow for control over network information flow, prevention of broadcast storms, enhanced security and protection of separate networks, cost-effectiveness, and easier management for IT staff.

## Part 2: Configure VLANs

### Create and Name VLANs on S1

I create and name VLANs on S1. The names are case-sensitive and must match the exact requirements:

- VLAN 10: Faculty/Staff

Commands used:

```plaintext
S1# (config) # vlan 10
S1# (config-vlan) # name Faculty/Staff
```

### Create the Remaining VLANs

I then create the additional VLANs:

- VLAN 20: Students
- VLAN 30: Guest(Default)
- VLAN 99: Management&Native
- VLAN 150: VOICE

Commands used:

```plaintext
S1# (config) # vlan 20
S1# (config-vlan) # name Students

S1# (config) # vlan 30
S1# (config-vlan) # name Guest(Default)

S1# (config) # vlan 99
S1# (config-vlan) # name Management&Native

S1# (config) # vlan 150
S1# (config-vlan) # name VOICE
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/64ea8e3d-6e6b-4afe-9839-f8688dc1a900" height="70%" width="70%" alt=""/>
</p>

### Verify the VLAN Configuration

I verify the VLAN configuration to ensure it is correctly set up.

#### Question:

Which command will only display the VLAN name, status, and associated ports on a switch?

The command `show vlan brief` will display the VLAN name, status, and associated ports.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0ed52e9f-d844-41da-aae0-46c06a782445" height="70%" width="70%" alt=""/>
</p>


### Create the VLANs on S2 and S3

I use the same commands from Step 1 to create and name the same VLANs on S2 and S3:

```plaintext
S2# (config) # vlan 10
S2# (config-vlan) # name Faculty/Staff

S2# (config) # vlan 20
S2# (config-vlan) # name Students

S2# (config) # vlan 30
S2# (config-vlan) # name Guest(Default)

S2# (config) # vlan 99
S2# (config-vlan) # name Management&Native

S2# (config) # vlan 150
S2# (config-vlan) # name VOICE
```

I repeat these commands on S3.

### Verify the VLAN Configuration

I close the configuration window and verify that the VLANs are correctly configured on S2 and S3.

<p align="center">
  <img src="https://github.com/user-attachments/assets/fa382c24-d579-488c-9742-582bbfeb570a" height="70%" width="70%" alt=""/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/fea6e45c-a955-4d90-bd9e-97ab8f842551" height="70%" width="70%" alt=""/>
</p>

## Part 3: Assign VLANs to Ports

### Assign VLANs to the Active Ports on S2

I configure the interfaces as access ports and assign VLANs as follows:

- VLAN 10: FastEthernet 0/11

Commands used:

```plaintext
S2(config)# interface f0/11
S2(config-if)# switchport mode access 
S2(config-if)# switchport access vlan 10 
```

I then assign the remaining ports to the appropriate VLANs:

- VLAN 20: FastEthernet 0/18
- VLAN 30: FastEthernet 0/6


<p align="center">
  <img src="https://github.com/user-attachments/assets/8e64789f-eb00-41e4-8b99-fb99b7a901ba" height="70%" width="70%" alt=""/>
</p>



### Assign VLANs to the Active Ports on S3

S3 uses the same VLAN access port assignments as S2. I configure the interfaces as access ports and assign VLANs as follows:

- VLAN 10: FastEthernet 0/11
- VLAN 20: FastEthernet 0/18
- VLAN 30: FastEthernet 0/6

<p align="center">
  <img src="https://github.com/user-attachments/assets/ba34bb95-7696-4b37-8b84-a12f1024f54a" height="70%" width="70%" alt=""/>
</p>

### Assign the VOICE VLAN to FastEthernet 0/11 on S3

The S3 FastEthernet 0/11 interface connects to a Cisco IP Phone and PC4. The IP phone has an integrated three-port 10/100 switch. One port is labeled Switch (connects to F0/4), another is labeled PC (connects to PC4), and there is also an internal port for IP phone functions.

I configure the S3 F0/11 interface to support user traffic to PC4 using VLAN 10 and voice traffic to the IP phone using VLAN 150. I also enable QoS and trust the Class of Service (CoS) values assigned by the IP phone:

```plaintext
S3(config)# interface f0/11
S3(config-if)# mls qos trust cos
S3(config-if)# switchport voice vlan 150
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/b1e8e872-ad73-46ad-8165-90829dd1afa5" height="70%" width="70%" alt=""/>
</p>

### Verify Loss of Connectivity

Previously, PCs on the same network could ping each other successfully. I study the output of the following command on S2:

```plaintext
S2# show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
99   Management&Native                active    
150  VOICE                            active     
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/b55fc6a5-2e2b-4f93-8a1e-1cb83cea2684" height="70%" width="70%" alt=""/>
</p>


#### Questions:

Although the access ports are assigned to the appropriate VLANs, were the pings successful?

No, the PCs are in the wrong VLAN.

What could be done to resolve this issue?

Since there will be inter-network activity, switch the ports to Trunk mode.
```
