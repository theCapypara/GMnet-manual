4. Client
---------

Client create event
~~~~~~~~~~~~~~~~~~~

**To create the udphp client** with **udphp\_createClient** you need a
**UDP socket (not server!)**, a **buffer**, as well as the **server
ip**. The rest is explained in the argument listing: ***How to use
udphp\_createClient (arguments)***:

-  **UDP client socket** - A UDP socket
-  **Server IP(string)** - The IP of the server to connect to (not the
   master server ip!)
-  **buffer** - A buffer
-  **directconnect(bool)** - If you set this to true, GMnet PUNCH will
   be bypassed. The client willdirectly connect to the server without
   hole punching. directconnect is automatically set to true when the
   master server is down or the server is not registered at the master
   server
-  **server\_port(real)** - This is optional. Set to 0 when unkown. This
   will be used (and is then required for successful connection) when
   the client connects directly and ONLY then. See above to know when it
   connects directly.

**IMPORTANT:** The function will **return the client id you have to
store**. This id is used to identify this client. Using this you can run
multiple clients in one game (as used in the demo). It will return -1 if
the client could not be created.

::

    buffer = buffer_create(256, buffer_grow, 1);
    client = network_create_socket(network_socket_udp);

    client_id = udphp_createClient(client,server_ip,buffer,false,1234);
    if (client_id < 0) {
        //Client could not be created. Destroy instace. GMnet PUNCH will also show a message if not silent.
        instance_destroy();
    }
    `

Client step event
~~~~~~~~~~~~~~~~~

**In the step event** simply run **udphp\_clientPunch** with the
**stored client id as argument**. This function will return false if the
client’s connection failed. This is the only way to determine if a
connection process failed and it will return true in all other cases.

::

    if (!udphp_clientPunch(client_id)) {
        //When this returns false, the connection failed or the client was destroyed.
        show_message("Connection failed!");
        instance_destroy();
    }
    `

Client networking event
~~~~~~~~~~~~~~~~~~~~~~~

**In the networking event simply call udphp\_clientNetworking with the
client id as an argument.**

Client: Get IP anf Port of server / check if connected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To communicate with the server after you are connected you of course
need **IP and port of the server**, you also need to know **if you are
already connected**. To do that use these functions:

::

    var connected = udphp_clientIsConnected(client_id); //true or false
    if (connected) {
       //The next functions will return invalid information if you use them without making sure you are connected:
       var ip = udphp_clientGetServerIP(client_id); //String
       var port = udphp_clientGetServerPort(client_id); //real
    }

Please see the hello world demo scripts in obj\_client for an example.

GMnet PUNCH is now set up!
~~~~~~~~~~~~~~~~~~~~~~~~~~

In the next page we will show the last feature: The online lobby!

--------------

**» Next topic: `Done! <tutorial/5_lobby>`__**

« Previous topic: `Server <tutorial/3_server>`__
