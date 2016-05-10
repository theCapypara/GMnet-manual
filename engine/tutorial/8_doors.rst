A second room and doors
-----------------------

Now you know nearly everything needed to make a very simple multiplayer
game.

The next sections will cover the following more advanced, but still not
very difficult, topics:

-  Using the multiplayer engine with mutliple rooms
-  Working with the data of the multiplayer engine

We are now going to **create a second room**. Simply\*\* copy\*\*
``htme_rom_demo`` and restructure the walls a bit. Maybe you could also
change the background color. **Remove all other objects from the room,
except the walls and ``htme_obj_network_controller``.**

There are two aproaches you could use if you want the player to enter
this room:

1. Place a new player instance in ``htme_rom_demo2``, make the player
   object NOT persistent
2. Make the player instance persistent; Persistent objects in Game Maker
   exist even after you change the room.

For this tutorial we are using the **second approach**. The reason for
that, is that we also want to teach you, how persistent objects work
with the instance. But if you solve your game using the first method,
this should also work in most cases. Please note that the second
approach is recommend though.

**Make your ``htme_obj_player`` persistent**. That's all we need to do
in the player object if we want him to move to a second room.

Now **create the object** ``htme_obj_door`` with the
sprite\ ``htme_spr_door``.

Create a **Collsion with ``htme_obj_player`` event** and add this code:

.. code-block:: gml

    ///CHECK IF DOOR ENTERED
    var isLocal;
    with (other) {isLocal = htme_isLocal();}

    if (isLocal && keyboard_check_pressed(vk_up)) {
        var dest = htme_rom_demo2;
        if (room == htme_rom_demo2) dest = htme_rom_demo;
        room_goto(dest);
    }

This checks when a player is standing in front of a door if the other
instance, which is an instance of the object ``htme_obj_player`` is our
local player by storing this information in the local variable
``isLocal``. When it's our local player ("we") we change the room. The
room is changed to ``htme_rom_demo2`` when in ``htme_rom_demo`` and
viceversa. **Place a door in each room**.

**We are done.**

Now start a client and server again and try switching rooms. Everything
should work as you would expect it. If not, check again if you made the
player object persistent and make sure the doors are on the same
position in both rooms.

Some technical stuff
~~~~~~~~~~~~~~~~~~~~

When you make persistent objects, they are only persistent locally.

That means when another player switches room, they will cease to exist
in your game. When you enter the room they will be resent and recreated
to your client.

Here is a nice little table **FOR AN INSTANCE CREATED BY A IN ROOM 1**:

.. figure:: images/2v2.PNG
   :alt: The table

   The table

We will extend this table later with a third scenrio that makes the
instances visible/existent at all time for all players.