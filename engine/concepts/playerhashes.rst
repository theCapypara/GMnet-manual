Players and Playerhashes
------------------------

Players are identified by hash strings.

You can loop through all players using this loop over the list returned
by `htme\_getPlayers <functions/tools/htme_getPlayers>`__:

.. code-block:: gml

    var playerlist = htme_getPlayers();
    for(var i = 0;i<ds_list_size(playerlist);i++) {
        var player = ds_list_find_value(playerlist,i);
    }

| ``player`` will contain the hash of the player.
| This hash can be used by
  `htme\_findPlayerInstance <functions/tools/htme_findPlayerInstance>`__.

You can get the local player (your player) hash by using the variable ``global.htme_object.playerhash``.

You can get a player hash from a synced object by using the objects variable ``obj_name.htme_mp_player``.
