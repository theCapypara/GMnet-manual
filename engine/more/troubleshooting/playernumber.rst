Player numbers
--------------

It can be tricky to get the player number. But here is how to do it.

Get current player
~~~~~~~~~~~~~~~~~~

Use this code to get the local player number. If you are the server your number is 1.
If another player connects he is number 2. If you have 3 players and p2 disconnect nr 2 is free.
When someone joins he will get the free nr 2.

.. code-block:: gml

    htme_getPlayerNumber(global.htme_object.playerhash);

Get remote player number from object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can also get the player number from any synced object. Use this code to check what player a synced object belongs to.

.. code-block:: gml

    htme_getPlayerNumber(obj_synced_player.htme_mp_player);
