### Delay Tolerant Networking Simulato made with python

## Introduction

This code allows you to simulate how to send packets in a network with a time delay using a python script. 
It is a modified version of the code from [PyDTNsim](https://github.com/ducktec/pydtnsim). The code uses qsim for an event driven simulation.

## Setup

Install the following Python packages using pip
    
    ```
    pip install networkx
    pip install tqdm
    pip instaall jsonschema
    ```

## Basic Structure of working

The program is divided in three fundamental units. Packets, Contacts and Network Nodes.

A Network Node is an object that can send and receive packets. It has a list of contacts that it can use to send packets. It also has a list of packets that it has received. Each node will have a limbo queue that contains any packets that have failed to be transmissted. Thic can be used later to implement a store and forward mechanism.

A Contact is an object that has a start time, end time and a capacity. It also has a list of packets that it has received. One node can contain multiple contacts based on the number of nodes it is connected to.

A Packet is an object that has a source node, destination node, size and a creation time. It also has a list of nodes that it has visited.
A Packet does not do any simulation work and is instead used to simulate the movement of packets in the network.

Packet Generator is an object that generates packets and adds them to the network. It has a list of nodes that it can send packets to. It also has a list of packets that it has generated.(It is an internal representation and is not used in the simulation in a front end sense.


## Limitations/Simplifications
The following limitations are known (not conclusive):
* No fragmentation is performed at node level. The packets are either fitting into the remaining bandwidth available in an contact or they are scheduled for another contact. The remaining bandwidth might be used by another smaller packet. By keeping the packet size small (and choosing suitable packet sizes and contact capacities), fragmentation side effects can be entirely avoided.
* No header overhead (let alone the header overheads of the Convergence Layers) are calculated and considered during the simulation. The simulation is routing-focused and thus disregards these factors.
* For now, no latency is considered during routing and is instead accounted for in the nodes itself. 
