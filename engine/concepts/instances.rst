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

Remember that all code outside the ``htme_isLocal`` will run on the remote computer.
This is because when the ``htme_obj_player`` sync to the other computer his game will create the same object.
So the create event, step event all events will run on his computer too. So you must make sure that you only run what you
want on the remote computer.
Ex in the ``htme_obj_player`` you have this code and this will run when you start the game

.. code-block:: gml

    // This code will run on your computer
    // *************************
    self.pressed_jump = false;
    self.pressed_left = false;
    self.pressed_right = false;
    self.name = "";
    // *************************

    // This code will run on your computer
    // *************************
    if (htme_isLocal()) {
        var ttr = totro(5,7,1);
        self.name = ttr[0];
        self.image_blend = irandom(16777215);
    }
    // *************************

The ``htme_obj_player`` is synced to all other player and will be created with ``instance_create(x,y,htme_obj_player)``.
And you know that when you create an object all events will run. So this will run on the remote computer: 

.. code-block:: gml

    // This code will run on the remote computer
    // *************************
    self.pressed_jump = false;
    self.pressed_left = false;
    self.pressed_right = false;
    self.name = "";
    // *************************

    // This code will not run because htme_isLocal()=false with a remote object on a remote computer
    // *************************
    if (htme_isLocal()) {
        var ttr = totro(5,7,1);
        self.name = ttr[0];
        self.image_blend = irandom(16777215);
    }
    // *************************

The other players will also sync their ``htme_obj_player`` to you so this will run on your computer:

.. code-block:: gml

    // This code will run on your computer
    // *************************
    self.pressed_jump = false;
    self.pressed_left = false;
    self.pressed_right = false;
    self.name = "";
    // *************************

    // This code will not run because htme_isLocal()=false on your computer with a remote object
    // Your computer is a remote computer in the other players perspective
    // *************************
    if (htme_isLocal()) {
        var ttr = totro(5,7,1);
        self.name = ttr[0];
        self.image_blend = irandom(16777215);
    }
    // *************************

As you can see there is a perspective. In your case all other players object is a remote object and you are local.
But in all other players perspective you are the remote and they are the local.