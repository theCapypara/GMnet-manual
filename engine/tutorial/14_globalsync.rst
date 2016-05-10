Bonus: Global Sync
------------------

The `update to version 1.1 <more/update>`__ added a new feature called
"Global Sync".

Before you learned how to sync instances between games in this tutorial.
However this concept has one downside: **Instances are only created and
controlable by one client.** All variables of an instance are
**read-only** to all other clients. That's why we needed to create a
seperate chat instance for each player that basicaly all jut synced one
chat variable. That may be fine for a few variables, and in this case
maybe even the best way of doing it, since every player still needs one
"chat outbox", however **you can now sync global variables that are
read- and writeable by all clients at all times.**

Summary of Global Sync's features: **Change the value on one end and it
will update on all other ends as well. All ends can update and access
all variables**

How it works
~~~~~~~~~~~~

It's super simple. **To store a variable** in the Global Sync pool use
this little code:

.. code-block:: gml

    var value = 1+1;
    htme_globalSet("name",value,buffer_u8);

The third argument is the `Buffer type/data type <concepts/buffer>`__.

This will now sync to all clients immediately (using the SMART
`syncType <concepts/synctypes>`__.).

You can **retrieve this variable** via this code **on all connected
clients and the server**:

.. code-block:: gml

    var value = htme_globalGet("name")

Please note that this function may return ``undefined`` if it wasn't set
by any of the clients/server yet, so check if it is defined:

.. code-block:: gml

    if (is_undefined((htme_globalGet("name")) {
        //Nope, that wasn't set yet...
    }