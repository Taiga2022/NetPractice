*This project has been created as part of the 42 curriculum by tshimizu.*

# NetPractice

## Description

NetPractice is a practical introduction to IPv4 networking. The project consists of ten browser-based exercises in which an incomplete network must be configured so that every communication objective succeeds.

The exercises cover:

- TCP/IP and IPv4 addressing
- CIDR notation and subnet masks
- Network, host, and broadcast addresses
- Default gateways and routing tables
- Communication through switches and routers
- The role of the network layer in the OSI model
- Forward and return paths between hosts and the Internet

There is no program to compile. The result of each level is exported as a JSON configuration file.

## Instructions

### Run the training interface

From the repository root, run:

```sh
cd net_practice
./run.sh
```

The script starts a local web server and normally opens the training interface in a browser. If it does not open automatically, start the server manually from the `net_practice` directory:

```sh
python3 -m http.server 49242
```

Then visit [http://localhost:49242](http://localhost:49242). The port may be changed if `49242` is already in use.

### Complete and export a level

1. Open the **Training** tab and enter the correct 42 login.
2. Change the unshaded fields in the network diagram.
3. Select **Check again** and use the logs to diagnose invalid addresses, missing gateways, or routing errors.
4. When every objective reports `OK`, select **Get my config** before moving to the next level.
5. Repeat the process for all ten levels.

The same login should be used throughout the training because it determines the generated configurations.

### Submission

Place the ten exported configuration files at the repository root, one file per level:

```text
level1.json
level2.json
level3.json
level4.json
level5.json
level6.json
level7.json
level8.json
level9.json
level10.json
```

Only files present in the Git repository are evaluated. Check the filenames, commit all ten files, and push them before submission.

During the defense, three random levels must be completed within the time limit. External tools are prohibited during the evaluation; only a simple calculator such as `bc` is tolerated.

## Networking notes

### IPv4 addresses and subnet masks

An IPv4 address identifies an interface. A subnet mask divides that address into a network part and a host part. Two directly connected interfaces can communicate when each considers the other to be on its local subnet and their addresses are unique.

The network address and broadcast address cannot normally be assigned to hosts. For example, `192.168.1.64/26` has the following range:

```text
Network address:    192.168.1.64
Usable hosts:       192.168.1.65 - 192.168.1.126
Broadcast address:  192.168.1.127
```

Common masks used in the exercises are:

| CIDR | Subnet mask | Addresses | Usable host addresses |
| ---: | --- | ---: | ---: |
| `/24` | `255.255.255.0` | 256 | 254 |
| `/25` | `255.255.255.128` | 128 | 126 |
| `/26` | `255.255.255.192` | 64 | 62 |
| `/27` | `255.255.255.224` | 32 | 30 |
| `/28` | `255.255.255.240` | 16 | 14 |
| `/29` | `255.255.255.248` | 8 | 6 |
| `/30` | `255.255.255.252` | 4 | 2 |

### Switches, routers, and gateways

A switch connects interfaces within the same local network. It does not route traffic between different IP networks.

A router connects different networks. Each router interface belongs to the subnet attached to it. When a destination is outside a host's local subnet, the host sends the packet to a directly reachable default gateway. Routers then use their routing tables to select the next hop.

A valid route needs both a destination network and a reachable next-hop address. Communication also requires a return path; a correct forward route alone is insufficient.

The default route is written as `0.0.0.0/0` and is used when no more specific route matches the destination.

### OSI model

NetPractice mainly concerns OSI Layer 3, the network layer, where IPv4 addressing and routing operate. Switches primarily forward frames at Layer 2, while routers forward packets between Layer 3 networks. Thinking about these roles helps separate local-link problems from routing problems.

## Troubleshooting checklist

- Verify that directly connected interfaces are in compatible subnets.
- Check for duplicate IP addresses.
- Do not assign a network or broadcast address to a host.
- Ensure that every gateway is reachable from the interface using it.
- Confirm that a route matches the intended destination.
- Check the return route as well as the forward route.
- Avoid masks so broad that a remote destination is mistaken for a local one.
- Read the interface logs after selecting **Check again**.

## Resources
- https://note.com/syamashi/n/n57fc506e0c5c


AI was used to review the subject requirements, organize the README, and improve the explanations of subnetting, gateways, routing, switches, routers, and OSI layers. The exported level configurations were completed separately and were not generated by AI.
