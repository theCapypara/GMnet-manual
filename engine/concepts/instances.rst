Local and remote Instances
--------------------------

When you **place an instance of an object into a room**, that is set up
to be be **synced via GMnet ENGINE**
(`mp\_sync(); <functions/sync/mp_sync>`__ called in the create-Event),
you will have **one local instance of this object in your room**, **and
one remote instance for each other player you are connected to**.

That means,\*\* if you place one instance of object A in your room\ **,
you will have** 4 instance if 4 players are playing\ **. Each player has
**\ one local instance he controls\ **, and the **\ three other
instances that the other players control\*\*.

You can find out if a instance is local by using
`htme\_isLocal(); <functions/tools/htme_isLocal>`__ by using this
if-Statement:

.. code-block:: gml

    if (htme_isLocal()) {
     //Bla
    }

everything in the statement will only be executed once for every player,
by the instance that he controls.

If you place 2 instances of an object into the room, you will have 8
instances with 4 players, of which 2 are local and the above code will
be executed by these two instances.
