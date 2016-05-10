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
    if (!htme_isStarted()) {
        show_message("Game Server or Client died! Restarting game...");
        game_restart();
    }

If ``htme_isStarted()`` **returns false** at any point after your client
connected to the server, you can be very certain, that you **lost
conection** to the server. Into the if Statement, simply put your own
code to handle this scenario. ``htme_isStarted()`` should always return
true for the server, unless the server dies due to an errror.

Oh, and don't forget to put the object into the ``htme_rom_demo``.