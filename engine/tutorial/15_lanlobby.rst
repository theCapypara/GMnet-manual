Bonus: A LAN lobby
------------------

.. note:: This topic requires GMnet PUNCH enabled.

\*\ **NOTE:** In addition to LAN lobbys, there are also `ONLINE
lobbys <tutorial/13_lobby>`__!

In addition to online lobbys, you can now also create LAN lobbys. In
this tutorial we will explain how. We'll assume you haven't read the
online lobby tutorial, but if you have: Creating a LAN lobby is
similiar, but there are some key differences.

This part of the tutorial will explain everything you'll need to know.
Before we start, please **create a new project and load the sample
project** (add all files from the GMnet ENGINE asset). ###Testing the
lobby

When you **press K when starting the game** you will be brought to the
demo lobby room. This is a very simple demo room that can only show four
servers. Once we are done, you'll be able to create an even better
lobby.

To test it, fire up a demo game on another PC in the network and start a
server. You'll see the server in the list after a few seconds.

The new concepts: Gamenames
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**(This is the same text as in the online lobby tutorial**)

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

**(This is the same text as in the online lobby tutorial**)

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

Setting broadcast settings.
~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default the servers will broadcast their information to all PCs in
the LAN each 15 seconds. You can change this in ``htme_config`` by
changing the value of ``self.lan_interval``

.. code-block:: gml

    /** 
     * Interval the servers broadcast data to the LAN, for the LAN lobby
     * @type real
     */
    self.lan_interval = 15*room_speed;

Building the lobby
~~~~~~~~~~~~~~~~~~

Ah, the lobby. Finally we are ready to build it.

The room of the lobby is the room ``htme_lanlobby``. This room only
contains the object ``htme_obj_lanlobbydemo``. This object controls the
lobby. Let's dive into it!

The create event
^^^^^^^^^^^^^^^^

.. code-block:: gml

    self.game = "htme_demo121"
    //IF YOU USE YOUR OWN SERVER - Change self.game!

    ///Recieve lobby data from the master server
    htme_startLANsearch(real(get_string("On which port should we search for servers?","6510")),self.game);

This will start searching the LAN for games with the game id
``self.game`` on the port that is asked to the player. More information
on this function can be found in the `usage page of
htme\_startLANsearch <functions/tools/htme_startLANsearch>`__.

The Room end event
^^^^^^^^^^^^^^^^^^

.. code-block:: gml

    ///STOP LAN SEARCH
    htme_stopLANsearch();

This will stop searching for LAN servers. You should run this if your
player leaves the lobby

The networking event
^^^^^^^^^^^^^^^^^^^^

.. code-block:: gml

    ///LOOKING FOR INCOMING SERVER BROADCASTS
    //htme_step doesn't do that btw!
    htme_networking_searchForBroadcasts();

This runs the code that actually searches for LAN servers. It waits for
incoming server broadcasts.

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
    var l = htme_getLANServers();
    for (var i = 0; i<4;i++) {
        draw_text(10,85+80*i,"=("+string(i+1)+")=");

First, the list ``htme_getLANServers()`` is stored in the local variable
``l`` (because it's shorter). **This ds\_list contains all the servers
we found**. It will be filled over time with all servers in the LAN.

Then it begins a loop that loops through the first 4 servers in the list
we got by the master server, everything is in this loop and then it
draws a nice little number for each server.

.. code-block:: gml

        if (ds_exists(l,ds_type_list)) {
            if (ds_list_size(l)>i) {

Now, this is the interesting part.

Ee check if it has at least as many entrys as the server we want to
list. For this example we assume ``i`` is 1. That means it checks if
there is atleast one server in the list. If yes, we have an entry we can
now draw.

.. code-block:: gml

                //Get stuff from the downloadlist
                var entry = l[| i];
                var ip = entry[? "ip"];
                var port = entry[? "port"];
                var game = entry[? "data1"];
                var servername = entry[? "data2"];
                var description = entry[? "data3"];

Now the entry (a ds\_map) for our server is extracted from the list and
we get the gamename, which is stored in data1, the ip, which is stored
in the key "ip", the name of the server, which we stored in data2, and
so on.

.. code-block:: gml

                draw_text(70,85+80*i,servername+" | "+ip+":"+string(port));
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
    var l = htme_getLANServers();
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
cancel. Although this is not needed if you filtered out other games with
htme\_startLANsearch like we did in the create event.

.. code-block:: gml

            if (htme_clientStart(ip, port)) {
                //Wait for connection success!
                room_goto(htme_rom_connecting);
            } else {
                show_message("Could not start client! Check your network configuration!");
            }
        } else {
          //Do nothing - There is no server on this slot
        }
    } else {
      //Do nothing - There is no server on this slot
    }

This is the rest of the script. We call ``htme_clientStart`` with the ip
we got from the list the port.

Afer that we just go to the waiting room. Done! The rest is the default
client connection you know and love.

And this is how you create a lobby! Now go ahead and do it! :)

Anything missing?
~~~~~~~~~~~~~~~~~

If this bonus chapter lacks something important, please let me know. If
you have any problems feel free to contact me. I know this is quite
complicated compared to the rest, so don't be frustrated when you have
problems.