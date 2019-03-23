# Peer---to---Peer-Distributed-

PROJECT REPORT
Group Information
1. Niraja Ganpule : UFID 17451951
2. Harshal Patil : UFID 55528581


Project Description
The main goal of this project is to implement Gossip and Push-sum algorithms which can be used for group communication as well as aggregate computation. In this project we have implemented these algorithms to run on the following topologies
1. Fully connected network
In a fully connected network all the nodes are connected to each other, every node knows every other node in the network.
2. Line topology
In a line topology, all nodes except the nodes at the two ends of the line will have exactly 2 neighbors, that is one on each side. The nodes at the end-points of the line will have only 1 neighbor.
3. Imperfect line
In this topology, each node has the same neighbors as in the line topology. Additionally, each node will have one more neighbor that will be randomly selected from the total number of nodes.
4. Random 2D grid
This topology consists of randomly distributed nodes on a grid of size [0-1.0] X [0-1.0]
The neighbors of each node will be all points that are at a distance of 0.1 or lesser from the node.
5. 3D Grid
In this topology, the nodes form a 3D grid. The neighbors of each node are the grid neighbors of that node.
6. Torus
In this topology, the nodes form a torus. The neighbors of each node are the torus neighbors.
The following algorithms have been implemented in this project
1. Gossip Algorithm for information propagation
The Gossip algorithm involves the following:
• Starting: A participant(actor) it told/sent a rumor(fact) by the main process
• Step: Each actor selects a random neighbor and tells it the rumor
• Termination: Each actor keeps track of rumors and how many times it has heard the rumor. It stops transmitting once it has heard the rumor 10
2. Push-sum Algorithm
The Push-sum algorithm is specified as:
• State: Each actor Ai maintains two quantities: s and w. Initially, s = i (that is actor number i has value i,) and w = 1
• Starting: Ask one of the actors to start from the main process.
• Receive: Messages sent and received are pairs of the form (s, w).
• Upon receive, an actor should add received pair to its own corresponding values. Upon receive, each actor selects a random neighbor and sends it a message.
• Send: When sending a message to another actor, half of s and w is kept by the sending actor and half is placed in the message being sent to the selected actor, the actor also sends the same message to itself (as stated in the paper)
• Sum estimate: At any given moment of time, the sum estimate is s/w where s and w are the current values of an actor.
• Termination: If s/w ratio of any actor did not change more than 10−10 in 3 consecutive rounds the actor terminates.
Running the code
Build
The code can be built by opening a terminal in the project directory and typing : mix escipt.build
Run
To run, enter the command escript proj2 <numberofnodes> <topology> <algorithm>
1. numberofnodes can be any natural number
2. topology is one of : full , line, impline ,rand2D,3D,torus
3. algorithm is one of : gossip, push-sum
Implementation
1. Main.ex
This file is the entry point to the code , containg the main method . It parses the commandline input and based on input it makes a function call to the corresponding function for that algorithm and topology combination
2. Logic.ex
This file contains the math for every protocol and topology combination.
Based on the input, the topology is built and the appropriate algorithm is run on this topology.
Besides the code for detecting how many of the actors reached their converging criteria and for displaying the time required for this convergence in milliseconds is housed in this file.
3. Gserver.ex
This file contains the business logic for each actor for the push-sum protocol.
It contains code regarding how the actor is spawned, how it is initialized, what it does when it receives a message,how it checks if it has achieved the convergence criteria and what it does once this happens.
4. Pserver.ex
This file contains the business logic for each actor for the Gossip protocol.
It contains code regarding how the actor is spawned, how it is initialized, what it does when it receives a message,how it checks if it has achieved the convergence criteria and what it does once this happens.
