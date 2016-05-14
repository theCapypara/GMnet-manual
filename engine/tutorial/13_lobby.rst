Bonus: An ONLINE lobby
----------------------

.. note:: This topic requires GMnet PUNCH enabled.

***NOTE:** Version 1.2.0 introduced `LAN
lobbys <tutorial/15_lanlobby>`__. This chapter only covers the online
lobby*

The `update to version 1.0 <lobbyupdate>`__ introduces a new lobby
system for online servers.

That means you can now add an online lobby to your game.

This part of the tutorial will explain everything you'll need to know.
Before we start, please **create a new project and load the sample
project** (add all files from the GMnet ENGINE asset).

We now have everything we created in this tutorial and more. The lobby
is one of these things. Let me take you on a tour on how it works.

**GMnet PUNCH needs to be activated. Please follow chapter 2 and 3 for
this.**

Testing the lobby
~~~~~~~~~~~~~~~~~

When you **press L when starting the game** you will be brought to the
demo lobby room. This is a very simple demo room that can only show four
servers. Once we are done, you'll be able to create an even better
lobby.

To test it, see if a server is online and connect to it via the lobby.
Please note that you have to set up a master server before, as explained
in chapter 3. If you use the demo master server, please note that there
might be "GMnet PUNCH Demo Servers" in the server list. You can not join
them, they were created using the UDPHP demo project. Both use the same
lobby and the same demo master server.

You can also create a server and fire up a second game and see if you
can join it.

The new concepts: Gamenames
~~~~~~~~~~~~~~~~~~~~~~~~~~~

In ``htme_config`` there is a new variable you need to change when
creating your own game (keep the default for the demo project though,
otherwise you can't join demo servers via the lobby):

.. code-block:: gml

    /**
     *  Shortname of this game
     *  + version
     *  Example: htme_demo100
     **/
    self.gamename = "htme_demo100"

This string represents your game and the version of your game. If you
update your game and it's server is not compatible with older versions,
change this string and you can prevent players from joining older
servers in the lobby (Please note that this is only for the lobby, if
your players are able to connect manually, you need to implement your
own way of kicking him out of the game again after he has connected, see
*How can my clients get the gamename and data strings after they
connected?* below for more info)

You can change it at any time, for example if you have multiple
gamemodes you want to mark in the lobby via ``htme_setGamename(name)``
and get it via ``htme_getGamename()``.

Data strings
~~~~~~~~~~~~

Asside from the gamename string, there are 7 more strings that can be
used to identify your game in the lobby.

Start the demo game and create a server. You will be asked to enter
**the name of the server and a description**. These are data strings 2
and 3. The demo lobby uses them for these purposes, but when making your
own game, you can use them however you want. 4-8 are unused by the demo
project.

Let's open the **N-key** event of **htme\_obj\_menu** (this event
creates the server).

You'll find this part after the server has successfully been created:

.. code-block:: gml

    htme_setData(2,get_string("How should this server be called (for the lobby)?","GMnet ENGINE Demo Server"));
    htme_setData(3,get_string("Enter a server description (for the lobby)?","A server created for the GMnet ENGINE demo project"));

As you can see, we set the server name and description right after the
server was started using ``htme_setData(n,string)``. We use 2 for server
name and 3 for description. You can also on the server end retrieve
these strings using ``htme_getData(n)``.

If you want to update any data string later, after the server connected
to the master server, you need to use ``htme_commitData()``. This syncs
all data strings to the master server. You MUST NOT use it here, because
the server hasn't connected to the master server yet!

A note for GMnet PUNCH users: The gamename is data string 1.

Building the lobby
~~~~~~~~~~~~~~~~~~

Ah, the lobby. Finally we are ready to build it.

The room of the lobby is the room ``udphhtme_lobby``. This room only
contains the object ``obj_udphphtme_lobby``. This object controls the
lobby. Let's dive into it!

The create event
^^^^^^^^^^^^^^^^

.. code-block:: gml

    //IF YOU USE GMnet PUNCH - it will only let you connect to GMnet PUNCH servers:
    if (!script_exists(asset_get_index("htme_init"))) {
       self.game = "udphp_demo120"
    }
    //IF YOU USE GMnet ENGINE - it will only let you conect to GMnet ENGINE servers
    else {
       self.game = "htme_demo121"
    }
    //IF YOU USE YOUR OWN SERVER - Change self.game!

    ///Recieve lobby data from the master server
    udphp_downloadServerList(4,"date","DESC",self.game);

First the variable ``game`` gets set. We use this to prevent GMnet
ENGINE players from joining GMnet PUNCH servers and vice-versa. As said
before, this object is used in GMnet ENGINE demo project and GMnet PUNCH
standalone demo project, this is why it has seperate code for both.

The important part here is
``[udphp_downloadServerList](functions/udphp_downloadServerList)``. This
will tell GMnet PUNCH (the part of the engine that controls
communication with the master server) to download a list of servers from
the master server. The paramters allow for filtering and sorting the
result, we use this to only get results that match our game name. More
information about what you can filter, can be found on the `usage page
of udphp\_downloadServerList <functions/udphp_downloadServerList>`__.

You use your own filtering variables later when creating your lobby.

The networking event
^^^^^^^^^^^^^^^^^^^^

.. code-block:: gml

    ///Waits for master server response
    udphp_downloadNetworking();

This code checks if the master server sent the server list and updates
it. This is not included in ``htme_networking();`` and therefor has to
be run here.

The draw event
^^^^^^^^^^^^^^

The draw event is split up into different sub-scripts:

'Background', 'Title and Controls', 'Online servers'
''''''''''''''''''''''''''''''''''''''''''''''''''''

Draws some background colors and some text, not important

'Servers (Loop)'
''''''''''''''''

This draws the actual server list.

Let's analyze it:

.. code-block:: gml

    ///Servers (Loop)
    var l = global.udphp_downloadlist;
    for (var i = 0; i<4;i++) {
        draw_text(10,85+80*i,"=("+string(i+1)+")=");

First, the list ``global.udphp_downloadlist`` is stored in the local
variable ``l`` (because it's shorter). **This ds\_list contains all the
servers we got from the master server**.

Then it begins a loop that loops through the first 4 servers in the list
we got by the master server, everything is in this loop and then it
draws a nice little number for each server.

.. code-block:: gml

        if (ds_exists(l,ds_type_list)) {
            if (ds_list_size(l)>i) {

Now, this is the interesting part.

First we check if the downloadlist was already created (it get's created
once the list has been downloaded). After that we check if it has at
least as many entrys as the server we want to list. For this example we
assume ``i`` is 1. That means it checks if there is atleast one server
in the list. If yes, we have an entry we can now draw.

.. code-block:: gml

                //Get stuff from the downloadlist
                var entry = l[| i];
                var ip = entry[? "ip"];
                var game = entry[? "data1"];
                var servername = entry[? "data2"];
                var description = entry[? "data3"];

Now the entry (a ds\_map) for our server is extracted from the list and
we get the gamename, which is stored in data1, the ip, which is stored
in the key "ip", the name of the server, which we stored in data2, and
so on.

.. code-block:: gml

                draw_text(70,85+80*i,servername+" | "+ip);
                draw_text(70,115+80*i,description);
            }
        }
        draw_line(0,160+80*i,room_width,160+80*i);
    }

Now we just draw everything.

'Footer'
''''''''

Again, just some text, not important.

The press 1-4 key events
^^^^^^^^^^^^^^^^^^^^^^^^

Pressing 1-4 on the keyboard will connect to that game. Let's see how!

.. code-block:: gml

    ///LOAD GAME SERVER ON SLOT 1
    var l = global.udphp_downloadlist;
    if (ds_exists(l,ds_type_list)) {
        if (ds_list_size(l)>0) {
            var entry = l[| 0];
            var ip = entry[? "ip"];
            var game = entry[? "data1"];

We again open the downloadlist and check if server 1 is in it, if yes we
continue.

.. code-block:: gml

            if (game != self.game) {
               //Not compatible game, exit
               show_message("Game server or version is incompatible!");
               exit;
            }

Remember the filtering variable we created in the create-event? We use
it here to check if the server is a GMnet ENGINE demo game. If not we
cancel. Please note, that this is propably not needed here, since we
filtered out all, but our game in the create event, when we ran
udphp\_downloadServerList.

.. code-block:: gml

            //====GMnet PUNCH DEMO ONLY
            if (!script_exists(asset_get_index("htme_init"))) {
               //This code is irrelevant for GMnet ENGINE and has been removed
            }
            //====GMnet ENGINE DEMO ONLY
            else {
                //Setup client, on success go to waiting room, otherwise end game
                //We don't actually know the port, but that doesn't matter, the master
                //server will tell us the port when we connect
                //
                //THE LINE BELOW is equivalent to:
                //if (htme_clientStart(ip, 0)) {
                if (script_execute(asset_get_index("htme_clientStart"),ip, 0)) {
                    //Wait for connection success!
                    room_goto(asset_get_index("htme_rom_connecting"));
                } else {
                    show_message("Could not start client! Check your network configuration!");
                }
            }
        } else {
          //Do nothing - There is no server on this slot
        }
    } else {
      //Do nothing - There is no server on this slot
    }

This is the rest of the script. We once again check if we are running
the GMnet ENGINE demo project and then we begin connection.

We call ``htme_clientStart`` with the ip we got from the list and leave
the port at 0. Why? Because we don't know the port. But that doesn't
matter, because when connecting to the server, GMnet ENGINE will
automatically resolve the port using UDPHP.

Afer that we just go to the waiting room. Done! The rest is the default
client connection you know and love.

And this is how you create a lobby! Now go ahead and do it! :)

How can my clients get the gamename and data strings after they connected?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now, you might want to get the datastrings and the gamename after you
connected. For example to display the name of the server in a corner, or
to make sure the server is comaptible to the client when connecting
manually.

For this you just create a object like the time syncing object. You sync
it with the engine, so all other players get it and sync 8 variables
that contain the value of the gamename string and the 7 data strings.

If you need help with that, contact me :)

Anything missing?
~~~~~~~~~~~~~~~~~

If this bonus chapter lacks something important, please let me know. If
you have any problems feel free to contact me. I know this is quite
complicated compared to the rest, so don't be frustrated when you have
problems.