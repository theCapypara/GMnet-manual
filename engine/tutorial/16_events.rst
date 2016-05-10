Bonus: Event Handlers for Connecting/Disconnecting
--------------------------------------------------

| Sometimes you may want to exceute code when players connect or
  disconnect. Or you want to prevent players from joining after the game
  has started.
| In this chapter, we will teach you how you can do that. It is very
  easy.

Basic example
~~~~~~~~~~~~~

Let's say you have this script called ``scr_welcome``:

.. code-block:: gml

    show_message("Cool! Someone connected!");
    return true; //- We will come to that later

You want to execute this script, if someone connects. To do that simply
use this code somewhere after the engine was started (obj\_htme is
created):

.. code-block:: gml

    htme_serverEventHandlerConnecting( scr_welcome );

That's all you have to do. For a script to be run at disconnection,
simply call ``htme_serverEventHandlerDisconnecting`` instead.

What is the return value for?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As you saw in the example above, the script ``scr_welcome`` returns
``true``.

If you are using a script as an event handler for **connecting**
players, you need to return either true or false (you don't have to
return anything for the Disconnect-Event).

| When your script returns **true**, the connection is **accepted** and
  the player is **connected**.
| When your script returns **false**, the connection is **refused** and
  the player will be **kicked** before he even really connected.

Getting more information about the player
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Both, the disconnect and connect event, provide an argument for your
script.

| The **connect event** gives your script an argument0 containing a
  **ds\_map** with the keys **port** and **ip**.
| The **disconnect event** also contains this ds\_map, but
  **additionally** has a key **hash** containing the `**player
  hash** <concepts/playerhashes>`__ that you can also use.

Here is an example how you can use this information. The server will
refuse all connections from the local computer when using this script:

.. code-block:: gml

    ///somewhere in your code
    htme_serverEventHandlerConnecting( scr_no_local_clients );
    htme_serverEventHandlerDisconnecting( scr_goodbye );

.. code-block:: gml

    ///scr_no_local_clients(player_map);
    var player_map = argument0;

    if (player_map[? "ip"] == "127.0.0.1") return false;
    else {
        show_message("Cool! "+player_map[? "ip"]+":"+string(player_map[? "port"])+" connected!");
        return true;
    }

.. code-block:: gml

    ///scr_goodbye(player_map);
    var player_map = argument0;

    show_message(":( ! "+player_map[? "ip"]+":"+string(player_map[? "port"])+" with the hash "+player_map[? "hash"]+" left!");