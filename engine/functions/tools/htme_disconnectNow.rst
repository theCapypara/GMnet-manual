``htme_disconnectNow()``
--------------------

Description
~~~~~~~~~~~

This will close and disconnect a server or client. This will also clean the engine and you can go to the main room if the script return true.
Use this when you want to exit the game and go back to the main menu.

.. code-block:: gml

    if htme_disconnectNow()
    {
        room_goto(rm_main);
    }

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

True if ok to disconnect.
