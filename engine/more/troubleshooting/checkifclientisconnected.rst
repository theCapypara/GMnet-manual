Check if client is connected
----------------------------

Sometimes you want to check if another player is conencted.

Use htme_getPlayers()
~~~~~~~~~~~~~~~~~~~~~

``htme_getPlayers()`` will return a ds list with all the connected players. 
You can check if above 1 and then you know a client is connected.

.. code-block:: gml

    var playerlist = htme_getPlayers();
    var total_players=ds_list_size(playerlist);
    if total_players>1 {
        show_debug_message("Another player is connected!");
    }
