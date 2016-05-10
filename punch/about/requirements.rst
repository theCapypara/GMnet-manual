Requirements
------------

Besides a valid **Game Maker: Studio** license you will also need to
host a master server somewhere. “Somewhere” means it has to be reachable
from the internet! [Ports must be opened] **Also please note that this
only works with UDP game servers!** - Setting up UDP game servers in
Game Maker is very differnt from TCP game servers since UDP is
connectionless. If you need help, contact me!

Wait, I need to host a “master server”?! - Where do I get that?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The server **GMnet GATE.PUNCH** that is needed to connect clients and
servers is free software and the source code can be found on it's
`product page <http://gmnet.parakoopa.de/gatepunch>`__.

It is written in java and you can either download the binarys or the
well-documented source code. Adjust the mediation server to fit your
needs or write your own (you can find the communication “protocol”
below) It comes with everything that is needed for TCP and UDP
communication with Game Maker: Studio and can also be used to create a
dedicated multiplayer server or something elese.

You need to host this server yourself. If you can’t right now, contact
me, I can host a server for you for testing purposes. For the demo you
can also connect to the default IP and port (please note that this demo
server might be down).

If you need more help setting up the server, `check out the tutorial
page of GMnet ENGINE on this
topic <http://gmnet.parakoopa.de/manual/engine/tutorial/3_udphp2>`__.
