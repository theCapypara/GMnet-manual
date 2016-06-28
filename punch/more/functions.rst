Function reference
------------------

*These are very brief and incomplete information. Detailed information
can be found in the script files*

The following scripts are scripts **YOU as the game developer** use:

Setup:
~~~~~~

-  **udphp\_config**
   One-time setup script
   Usage:
   udphp\_config(master\_ip,master\_port,reconnect\_intv,timeouts,debug,silent,delta time,upnp)

Server:
~~~~~~~

-  **udphp\_createServer**
   To be used in the Create event of the server
   Usage: udphp\_createServer(udp\_server,buffer,player\_list,upnp port)
-  **udphp\_serverPunch**
   To be used in the step event of the server
   Usage: udphp\_serverPunch()
-  **udphp\_serverNetworking**
   To be used in the networking event of the server
   Usage: udphp\_serverNetworking()
-  **udphp\_stopServer**
   Usage: udphp\_stopServer()
   Delete the instance afterwards

Client:
~~~~~~~

-  **udphp\_createClient**
   To be used in the Create event of the client
   Note: Returns client id
   Usage:
   udphp\_createClient(udp\_socket,server\_ip,buffer,directconnect,directconnect\_port)
-  **udphp\_clientPunch**
   To be used in the step event of the client
   Usage: udphp\_clientPunch(id)
-  **udphp\_clientNetworking**
   To be used in the networking event of the client
   Usage: udphp\_clientNetworking(id)
-  **udphp\_stopClient**
   Usage: udphp\_stopClient(client\_id)
   Instance should be deleted with the false return value of clientPunch

Tools:
~~~~~~

-  **udphp\_clientGetServerIP**
   [for client] This will return the server ip of this client and should
   only be used if the client is connected.
   Usage: udphp\_clientGetServerIP(client\_id)
-  **udphp\_clientGetServePort**
   [for client] This will return the server port of this client and
   should only be used if the client is connected.
   Usage: udphp\_clientGetServerPort(client\_id)
-  **udphp\_playerListIP**
   [for server] Get an ip out of a player list entry (see serverCreate
   for details)
   Usage: udphp\_playerListIP(player)
-  **udphp\_playerListPort**
   [for server] Get an port out of a player list entry (see serverCreate
   for details)
   Usage: udphp\_playerListPort(player)
-  **udphp\_clientIsConnected**
   [for client] With this you can check if your client has conncted to
   the server.
   Usage: udphp\_clientIsConnected(client\_id)

Lobby:
~~~~~~

-  **udphp\_downloadServerList**
   [no server or client has to be running]
   Download a list of servers from the lobby. `More
   information <tutorial/5_lobby>`__.
   Usage: `See GMnet ENGINE manual
   page <http://gmnet.parakoopa.de/manual/engine/functions/lobby/udphp_downloadServerList>`__
