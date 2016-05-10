What is UDP hole punching?
--------------------------

**UDP hole punching** is a technique that allows UDP packets to be send,
that normally a NAT would block. Normally if you want to host a game,
you have to open the ports, because otherwise your NAT would block the
UDP (or TCP) packets that are required for network communication. UDP
hole punching works because in the process the client does not simply
“connect” to the server. The server also sends packets back, which means
both try to connect at the same time to each other. Then both NATs will
accept the connection.

The problem is that at least the server doesn’t know when a client
connects to it. That’s why we need a (globally reachable= master server.
The server registers at the master server and opens a TCP connection so
the master server can send the client informations\*. When a client
tries to connect, it also registers it’s UDP port at the master server
and tells it to which server it wants to connect. If the server is
found, the ports will be send backd via TCP. The client get’s the server
port/ip and the server the client port/ip. Then both send the packets
and the hole is punched. Both players are connected to each other.

(\* TCP allows the master server to send packets back to the server.
That’s because TCP works with connections and if the server opens a
connection to the master server, both can send packets to each other,
even if the server is behind a NAT.)

(Source: http://en.wikipedia.org/wiki/UDP_hole_punching)
