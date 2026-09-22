# Nmap — Week 1 Host Discovery Lab

## Overview

This lab introduces Nmap host discovery in an isolated VMware environment.

The purpose of the exercise is to identify active systems on an authorized subnet and compare Nmap discovery results with the known asset inventory.

## Lab Environment

The lab was built using VMware to create and manage the virtual machines.

- **Hypervisor:** VMware
- **Virtual Network:** VMnet2
- **Subnet:** `10.10.10.0/24`
- **Network Type:** Isolated lab network

See [Rules of Engagement](rules-of-engagement.md) for the complete authorized scope and testing limitations.

## Host Discovery

Nmap host discovery was first performed without elevated privileges:

```
nmap -sn -v --reason 10.10.10.0/24
```

The scan was then repeated with elevated privileges:

```
sudo nmap -sn -v --reason 10.10.10.0/24
```

### Options Used

* `-sn` — Performs host discovery without a port scan.
* `-v` — Enables verbose output.
* `--reason` — Displays the reason Nmap considers a host online.

## Results

The output from both discovery scans was saved for comparison:

* [`discovery-unprivileged.txt`](results/discovery-unprivileged.txt)
* [`discovery-privileged.txt`](results/discovery-privileged.txt)

The privileged scan successfully discovered the Windows target, while the unprivileged scan did not identify it during testing.

Because the targets are on the same local Ethernet network,
Nmap can use ARP-based host discovery when it has the required
privileges. This demonstrated how scan privileges and discovery
methods can affect host-discovery results.
## Asset Inventory

The known systems in the lab are documented separately in the [Asset Inventory](asset-inventory.md).

## Network Diagram

The lab topology is documented in the network diagram:

![Lab Network Diagram](diagrams/network-diagram.png)

*Diagram created using diagrams.net (draw.io).*

## Key Takeaways

* Nmap can identify active hosts on a network without performing a port scan.
* `-sn` is useful for initial host discovery.
* Scanner privileges can affect discovery behavior and results.
* A host that does not appear in a discovery scan should not automatically be considered offline.

