How to quit/disconnect
----------------------

When you start a server or connect a client to a server and want to quit while you are in the game.

Use htme_disconnectNow()
~~~~~~~~~~~~~~~~~~~~~~~~

After you call ``htme_disconnectNow()`` the gmnet engine will disconnect and you can go to the room you want.
Make sure you remove all other network related objects after.

.. code-block:: gml

    if htme_disconnectNow() {
        // If disconnect is ok then do some cleaning
        // Remove persistent but not synced objects
        with htme_obj_chat instance_destroy();
        with htme_obj_playerlist instance_destroy();
        // Go back to menu room
        room_goto(htme_rom_menu);    
    }
