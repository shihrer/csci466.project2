## Instructions
###### Due: 10/7/16 11:59PM

Complete the following assignment in pairs, or groups of three.  Submit your work into the Dropbox on D2Linto the "Programming Assignment 2" folder.  Both partners will submit the same solution and we will only grade one solution for each group.

## Learning Objectives

In this lab you will:

* Work with a layered network architecture.
* Understand and implement the Stop-and-Wait Protocol with ACK (Acknowledgments), NACK (Neg-ative Acknowledgments), and re-transmissions

## Assignment

During this project, you will implement the Reliable Data Transmission protocols RDT 2.1, and RDT 3.0 discussed in class and the textbook by extending an RDT 1.0 implementation.

## Starting Code

The starting code for this project (**prog2.zip** in the D2L content area) provides you with the implementation several network layers that cooperate to provide end-to-end communication.

    APPLICATION LAYER (client.py, server.py)
    TRANSPORT LAYER (rdt.py)
    NETWORK LAYER (network.py)

The client sends messages to the server, which converts them to pig latin, and transmits them back. The client and the server send messages to each other through the transport layer provided by an RDT implementation using the `rdt10send` and `rdt10receive` functions.  The starting `rdt.py` provides only the RDT 1.0 version of the protocol, which does not tolerate packet corruption, or loss.  The RDT protocol uses `udtsend` and `udtreceive` provided by `network.py` to transfer bytes between the client and server machines.  The network layer may corrupt packets or lose packets altogether.  `rdt.py` relies on the `Packet` class (in the same file) to form transport layer packets.  Your job will be to extend `rdt.py` to tolerate packet corruption and loss.  The provided code lists prototype send and receive functions for those protocols.  You may need to modify/extend the `Packet` class to transmit the necessary information for these functions to work correctly.  The provided implementation of `network.py` is reliable, but we will test your code with non-zero probability for packet corruption and loss by changing the values of `prob_pkt_loss` and `prob_byte_corr` of the `NetworkLayer` class.  You may change those variables yourself to test your code.

## Program Invocation
To run the starting code you may run:

    python server.py 5000
    python client.py localhost 5000
    
 Be sure to start the server first, to allow it to start listening on a socket, and start the client soon after, before the server times out.
 
 ## BONUS 1
 The network layer may also reorder packets.  If you set `prob_pkt_reorder` to a non-zero probability you will start seeing packets that are reordered.  I will award one bonus point to any group that implements RDT 3.1, which delivers packets in the correct order.
 
 ## BONUS 2
 The RDT 3.1 is a stop and wait protocol.  I will award one bonus point to any group that implements RDT 4.0 - a pipelined reliable data transmission protocol based on either Go-back-N (GBN), or Selective Repeat (SR) mechanisms.