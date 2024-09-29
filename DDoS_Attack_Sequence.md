```mermaid
sequenceDiagram

    participant User
    participant Attacker
    participant Botnet
    participant Cloud Flare Server

    Attacker -x Botnet: Assembles botnet network, infects machine with Malware
    Attacker ->> Botnet: commands and controls botnets to execute attack

    loop Attempts to spam until no more TCP ports available
    Botnet ->>+ Cloud Flare Server: Sends SYN packet to server port requesting communication
    Cloud Flare Server ->> Botnet: Returns SYN-ACK packet, leaves port open waiting for "handshake" ACK packet
    end
    
    Cloud Flare Server -x Botnet: Analyzes packets for attack patterns, tools, metadata and withholds transmission in cloud until confirmed or blocked

    User ->> Cloud Flare Server: Sends SYN packet to server port requesting communication
    Cloud Flare Server ->> User: Returns SYN-ACK packet to acknowledge the communication
    User ->> Cloud Flare Server: Returns ACK packet to acknowledge the packet receipts, TCP connection now open
    User ->> Server: User can connect to server and exchange data

```


    
In this scenerio, a business using cloud flare is being attacked by a SYN DDoS method

First the attacker infects external computer with malware for botnet

Then Attacker connects and executes command to carry out attack

The botnet Sends SYN packet to cloud server to request communications
Cloudflare will analyze packets, trying to detect attack patterns, concerning meta data, unconfirmed handshakes.
If cloudflare detects numerous SYN packets from specified IP's Cloudflare can limit the rate on specific IP adresses
Cloudlflare witholds packets from being sent to server until handshakes are confirmed and data is filtered.

If connection request is valid, its passed to server.