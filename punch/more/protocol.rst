GMnet PUNCH/GATE.PUNCH “protocol” (for building your own server)
----------------------------------------------------------------

This is a linear breakdown of what packets are sent:

| **SERVER:**
| -> Sends UDP packet to master server containing the string “reg” with
  the line feed character (unicode 10) at the end
| -> (Re-)connects via TCP to master server
| -> Sends TCP packet to master server containing the string “reg” with
  the line feed character (unicode 10) at the end
| -> Repeats every X minutes [alternative smethod is to reconnect when
  TCP socket is closed]

| **MASTER SERVER:**
| <- When recieving the UDP packet with “reg” the UDP port for that
  server get’s saved
| <- When recieving the TCP packet with “reg” this connection socket is
  saved so the master server can use it later to communicate with the
  server

| **CLIENT:**
| -> Sends UDP packet to master Server containing the string “connect”
  with the line feed character (unicode 10) at the end
| -> Opens TCP connection to master server
| -> Sends TCP packet to master Server containing the string
  “connect”+line feed+IP of the server we want to connect to+line feed

| **MASTER SERVER:** <- When recieving UDP packet with “connect” the UDP
  port for that client get’s saved
| <- When recieving TCP packet that has “connect” in the first line
  (unicode 10 is used as a newline).

-  WHEN FOUND:
   -> Via the client’s TCP socket: Send UDP ip&port of server to client
   [packet: buffer\_s8 (-1), buffer\_string (ip), buffer\_string (port)]
   -> Via the server’s TCP socket: Send UDP ip&port of the client to
   server [packet: buffer\_s8 (-1), buffer\_string (ip), buffer\_string
   (port)]
-  WHEN NOT FOUND:
   -> Send not found packet to client via TCP [packet: buffer\_s8 (-2)]

**CLIENT:** <- Wait for packet of master server

-  -> When id -2 (not found): Connect directly to the server
-  -> When id -1 (found): Save the two strings, convert the port to a
   real and connect to server via UDP and the recieved ip&port
   (Knock-Knock) [packet: buffer\_s8 (-3)]

**SERVER:** <- Wait for packet of master server

-  -> When id -1 (found): Save the two strings, convert the port to a
   real and connect to client via UDP and the recieved ip&port
   (Knock-Knock) [packet: buffer\_s8 (-3)]

<- Wait for incoming client Knock-Knock packet (-3):

-  -> When not already connected with this client: add it to the
   connected clients and send a welcome packet via UDP back to the
   client that sent this packet [packet: buffer\_s8 (-4)}

| **CLIENT:**
| -> When recieving the welcome packet: Mark client as connected.
| -> When not recieving a welcome packet after a timeout: Tell the
  player the connection failed

Without hole punching the client simply sends the Knock-Knock packets to
the server and waits for the servers welcome message.
