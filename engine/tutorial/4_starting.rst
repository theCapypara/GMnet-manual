Starting the engine
-------------------

Great! Now that we are set up, let's actually make a game.

Before we start, if you want to follow the tutorial make sure again,
that you added all sprites, all scripts and the object ``obj_htme`` to
an empty project.

The menu
~~~~~~~~

Let's create a very basic menu.

First create a **new room** called **htme_rom_menu**. For this
tutorial we are keeping things very basic and we are not using any views.
Set the **background color** to be **black** and the dimensions
of the room to be **800x600px**.

Add ``obj_htme`` to the room. This object should be created in the
first room of every game you create. It is persistent and will exist
even when you change the rooms.

Now **create** an object called ``htme_obj_menu``. This will control
our basic menu. Add it to the room we just created.

In the **Draw-Event** put the following code, that will simply display a
message on how to proceed when starting the game:

.. code-block:: gml

    draw_text(20,20,"Press N for new server and B to connect.");

Add two more events to it. One **B-key** event and a **N-key** event.
B will join a server and N create a new one.

Starting the server
^^^^^^^^^^^^^^^^^^^

In the **N-key** event add the following code:

.. code-block:: gml

    ///START SERVER

    //Ask player for port
    var port = real(get_string("On which port should the server listen?","6510"));

    //Setup server, on success start game, on failure end the game.
    if (htme_serverStart(port,32)) {
        room_goto(htme_rom_demo);
    } else {
        show_message("Could not start server! Check your network configuration!");
        game_end();
    }

This will first **ask the player** on which **port** the server should
run (of course you can also decide to specify a fixed port number).

After that it **starts the server** using
``htme_serverStart(port,maxplayers)`` on that port and allows a maximum
of **32 players**. It checks if the server is running, and if it is, it
**goes to the game room** that we will create in a second.

Starting the client
^^^^^^^^^^^^^^^^^^^

In the **B-key** event add the following code:

.. code-block:: gml

    ///CONECT TO A SERVER

    //Ask player for ip & port
    var ip = get_string("To which server should we connect?","127.0.0.1");
    var port = real(get_string("And on which port is the server running?","6510"));

    //Setup client, on success go to waiting room, otherwise end game
    if (htme_clientStart(ip, port)) {
        room_goto(htme_rom_connecting); //NOTE THAT WE ARE GOING TO ANOTHER ROOM HERE THAN THE SERVER ABOVE
    } else {
        show_message("Could not start client! Check your network configuration!");
        game_end();
    }

Now that is slightly more complicated. It **asks for both ip and port** and then tries to connect using
``htme_clientStart(ip, port)``.

Instead of going to the game room when we are done, we actually
want **the client to go to** ``htme_rom_connecting`` which is a room

we are now going to create. Why? This room will **display a message**
saying "Connecting..." and there will be an object in it that
**waits for the client to be connected**. After that we want to
go to the game room.

The waiting room ``htme_rom_connecting``
''''''''''''''''''''''''''''''''''''''''

**Create a room** called ``htme_rom_connecting`` that is just like the
first one (but without the objects in it). Now **create the object**
``htme_obj_waitforclient`` and **place it** into the room.

In the **Draw event** put the following code:

.. code-block:: gml

    draw_text(20,20,"Connecting...");

This will display the message "Connecting..." after the player decided
to start the client.

In the **Step-Event** put the following:

.. code-block:: gml

    ///Check if client is connected
    if (htme_clientIsConnected()) {
        room_goto(htme_rom_demo);
    }
    if (htme_clientConnectionFailed()) {
        show_message("Connection with server failed!");
        game_restart();
    }

The first statement used the ``htme_clientIsConnected()`` function to
check if the client is... well connected. If so, **we can finally go to the game room**.

If the global timeout has been reached, the engine gives up to conect.
In this case the second if-Statement is activated which uses
``htme_clientConnectionFailed()`` to check if the connection failed.
In our example it will simply restart the game.

This waiting room is just an example and you can use different
techniques to display a waiting... message.

Connection done!
----------------

Theoretically, we could now play the game. Of course, there is no game.
The game will crash if we try to start a server because our game room
``htme_rom_demo`` does not exist.

For now, **create an empty room** just like you did before and call it
``htme_rom_demo``.

Now, when you **fire up your game twice**, you should be able to **start
a server** on one game, which should **lead you to the empty room**.

On the **other game** you should be able to **connect to this server**
by connecting to the ip **127.0.0.1**. If it was successfull, the
"Connecting..." message should disappear, and you'll **find yourself in
the same empty room as the server**. **Yay!**