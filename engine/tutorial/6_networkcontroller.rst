The network controller
----------------------

Before we continue, let's create an object that makes sure, the engine
is still running.

The **engine will stop** running on the client-side, when the
**connection** between server and client is **lost**.

**Create the object** ``htme_obj_network_control``. Into the
**Step-Event** put the following code:

.. code-block:: gml

    ///Check if engine running
    if (htme_isLostConnection()) {
        htme_error_message_handler("Game Server or Client died! Go back to menu...");
    
        // Clean other persistent non synced objects from room
        with htme_obj_chat instance_destroy();
        with htme_obj_playerlist instance_destroy();    
    
        room_goto(htme_rom_menu);
    }

If ``htme_isLostConnection()`` **returns true** at any point after your client
connected to the server, you can be very certain, that you **lost
conection** to the server. Into the if Statement, simply put your own
code to handle this scenario. ``htme_isLostConnection()`` should always return
false for the server, unless the server dies due to an errror.

Oh, and don't forget to put the object into the ``htme_rom_demo``.