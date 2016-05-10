Adding a player
---------------

Okay, okay, I know we already added a player in Step 5.

| What this title means, is simply that we are now **adding the player
  to the engine**. After this step the player will be **synchronized
  between all players you connect to your server**.
| So we are basicly done after this step. The rest of the tutorial is
  some more advanced stuff.

The create event
~~~~~~~~~~~~~~~~

To set the player up, we only have to make minimal adjustments. **Create
a new code block in the create event**, and insert it **before** the
other block.

Start the code block with

.. code-block:: gml

    mp_sync();

This will **tell the engine to sync this object**. Once this was created
on one client, this instance wil also be **sent to all other players**.

If you add one player instance to your room and connect 4 players
togther, each player will have four player instances.

Now we need to tell the engine what variables to sync and how:

.. code-block:: gml

    mp_addPosition("Pos",5*room_speed);

This will tell the engine to sync the position variables ``x`` and ``y``
every 5 seconds. ``5*room_speed`` means 5 seconds. The first argument of
``mp_addPosition`` is the name of group. You can choose that however you
want.

What we just added is a so called **variable group**. The group is
called "Pos", get's synced every 5 seconds and sync the variables ``x``
and ``y``.

Let's set **how the position should be synced**:

.. code-block:: gml

    mp_setType("Pos",mp_type.SMART);

This changes the **sync type** to the variable group "Pos". **The
default sync type is FAST**. We are changing it to **SMART**. Here is a
list of what every sync type does:

-  **FAST** (default, you don't have to use ``mp_setType`` if you want
   to use that): In our case, if we had chosen FAST, the engine would
   send the position of our player every 5 seoncds **once**. Since we
   are using UDP for networking, there is no assurance, that it will
   actually arrive. That means we don't know if the other players
   actually get our position every 5 seoncds. The packet could get lost.
   However, using FAST is very... FAST. You will see when we want to use
   FAST later in this section.
-  **IMPORTANT**: When using IMPORTANT, in our case the position would
   still be synced every 5 seoncds. However, we are using a special way
   in *GMnet ENGINE* to make sure the packet arrives. Every 5 seconds,
   the server/client will flood the other players with the information,
   until they respond back, that they got it. That's how we assure the
   information is actually sent. This is however a pretty traffic heavy
   operation and using that in too short intervals will cause lagg in
   both connection and framerate.
-  **SMART**: This is like IMPORTANT but better. Instead of syncing
   every 5 seconds, we will only sync every 5 seconds what has changed.
   If only the x position changed, we are not syncing the y position. If
   our position has not changed at all, we are not syncing. This is
   basicly a more traffic-friendly version of IMPORTANT.

We are using **SMART** here and relatively large intervals, because we
only sync the position as a backup. As you will see later, we are going
to sync the button inputs every single step. **We only sync the position
to make sure, the players don't get desynchronized**.

The\*\* button input later will be synced FAST\ **. That means **\ some
packets could be lost\ **, and after some time the player could be on
two completly different parts of the level, depending on the complexity
of your platformer. To make sure that doesn't happen, **\ we reset the
position every 5 seconds\*\*.

Now, the thing is, if we reset it every 5 seconds, it might happen that
**the players are just some pixels off**. In that case our players might
**slightly "flicker"** whenever the position resets. **That doesn't look
nice**.

Let's add a little **tolerance range**. If the position at is **less
than 20 pixels away from where it should be**, the other players should
**not apply this change** locally, so it **doesn't flicker** that much:

.. code-block:: gml

    mp_tolerance("Pos",20);

Great. Position is set up. Now, **just to make sure**, let's also sync
**the basic Game Maker physics and drawing variable**\ s:

.. code-block:: gml

    /**
     * Tell the engine to add the basic drawing variables:
     * image_alpha,image_angle,image_blend,image_index,image_speed,image_xscale
     * image_yscale,visible
     */
    mp_addBuiltinBasic("basicDrawing",15*room_speed);
    mp_setType("basicDrawing",mp_type.SMART);

    /**
     * Tell the engine to add the builtin GameMaker variables:
     * direction,gravity,gravity_direction,friction,hspeed,vspeed
     */
    mp_addBuiltinPhysics("basicPhysics",15*room_speed);
    mp_setType("basicPhysics",mp_type.SMART);

We don't need to sync them that frequently. If we sync physics to
frequently that might look weird and we are only syncing the basic
Drawing stuff for the player color (``image_blend``) which doesn't
change anyway, and the ``image_xscale`` and ``iamge_angle`` which
controls how the player faces, which isn't that critical.

Now we also want to **sync the name**:

.. code-block:: gml

    mp_add("playerName","name",buffer_string,60*room_speed);
    mp_setType("playerName",mp_type.SMART);

This is using ``mp_add`` to sync our own variables. The syntax is
slightly more compelx and we need to do some things to make this work
later, but let's just see what we got here: \* The first argument is
again the name of the group \* In the second argument you specify the
**names of the variables** you want to sync, **seperated by commas**. We
stored the player name in the "name" variable. \* The third argument is
the **buffer type**. You can find information on which buffer type you
need to use on `this manual page <concepts/buffer>`__. **All variables
need to have the same buffer type.** ``buffer_string`` simply means that
the variable "name" stores a string. \* The last argument is the syncing
interval, just as before.

We decide for a 60 seconds interval, because the name will never change.
We could have also used 20 years, that wouldn't make a difference. We
only need to make sure the engine syncs it on login and some other
critical events, and it does that automatically, no matter what interval
we choose. We still need to make it SMART because we need to make sure
it REALLY arrived at those events.

Next up are the **controls**. Remember how we stored the button input in
seperate variables? Well now you might know why:

.. code-block:: gml

    mp_add("controls","pressed_jump,pressed_left,pressed_right",buffer_bool,1);

The "buffer type" is ``buffer_bool``, because our "pressed\_" variables
are booleans. 1/0, true/false.

This will **sync the button input to all players every single frame** no
matter what. We don't want to have it SMART or IMPORTANT. **FAST is the
way to go**, since there is **no point in checking if the data
arrives**, because we are syncing the button input every step anyway.

Some things needed when using ``mp_add``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| Since we are using ``mp_add`` to sync our own variables, we need to
  make some code changes. We need to send the variables to the engine at
  the beginning of the step, and retrieve the data at the end.
| The reason fot that is, that in Game Maker there is `no way of getting
  a variable's content by accessing it via a
  string <http://gmc.yoyogames.com/index.php?showtopic=646036&hl=>`__.
  We need to store the values to a map first before the engine can read
  them. This is not needed for ``mp_addPosition``,
  ``mp_addBuiltinBasic`` and ``mp_addBuiltinPhysics``, because we
  hardcoded them.

If you don't know what any of that means what I just said, don't worry.
It's complicated.

**The only things you need to know, we will explain them now:**

For every object where you use ``mp_add`` add the following to the
**begin step** event:

.. code-block:: gml

    mp_map_syncIn("name",self.name);
    mp_map_syncIn("pressed_jump",self.pressed_jump);
    mp_map_syncIn("pressed_left",self.pressed_left);
    mp_map_syncIn("pressed_right",self.pressed_right);

Replace the names with the names of your synced variables. These are the
variables that we created above for our tutorial player.

All changes to these variables need to be made **BEFORE** using these
functions. That means you either have to change them in begin step, or
call ``mp_map_syncIn`` again after you changed variables. We recommend
the first. And that's also what we are going to do in a minute.

In the **end step** event add the following code to retrieve the
variables again:

.. code-block:: gml

    self.name = mp_map_syncOut("name", self.name);
    self.pressed_jump = mp_map_syncOut("pressed_jump", self.pressed_jump);
    self.pressed_left = mp_map_syncOut("pressed_left", self.pressed_left);
    self.pressed_right = mp_map_syncOut("pressed_right", self.pressed_right);

Setting up controls for synchonization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Last thing we need to do, is to **move this code out of the step event**
we created earlier:

.. code-block:: gml

    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);

**Simply remove it**. In begin step, **add the following code**
**before** the other code:

.. code-block:: gml

    if (htme_isLocal()) {
        self.pressed_jump = keyboard_check(vk_space);
        self.pressed_left = keyboard_check(vk_left);
        self.pressed_right = keyboard_check(vk_right);
    }

It should now look like this:

.. code-block:: gml

    if (htme_isLocal()) {
        self.pressed_jump = keyboard_check(vk_space);
        self.pressed_left = keyboard_check(vk_left);
        self.pressed_right = keyboard_check(vk_right);
    }
    mp_map_syncIn("name",self.name);
    mp_map_syncIn("pressed_jump",self.pressed_jump);
    mp_map_syncIn("pressed_left",self.pressed_left);
    mp_map_syncIn("pressed_right",self.pressed_right);

All the code we just pasted in begin step does, is **check if this is
the instance that was locally created** and then **writes the button
input of the players into the variables**.

This way when we have 4 players, we only move the instance we control,
the instance we locally created. The ``self.pressed_jump...`` variables
will be changed by the other 3 players for the rest of the three
instances.

**Look at the following table from the view of player 1:**

+-------------------+--------------------------+------------------------------+
| Instance/Player   | Controlled via buttons   | Controlled via engine        |
+===================+==========================+==============================+
| Ours / Player 1   | Yes                      | No                           |
+-------------------+--------------------------+------------------------------+
| Player 2' s       | No                       | Yes, buttons from Player 2   |
+-------------------+--------------------------+------------------------------+
| Player 3' s       | No                       | Yes, buttons from Player 3   |
+-------------------+--------------------------+------------------------------+
| Player 4' s       | No                       | Yes, buttons from Player 4   |
+-------------------+--------------------------+------------------------------+

Test
~~~~

Fire up two games and create a server / connect to 127.0.0.1.

You should now see both players, **and should see that we now have a
multiplayer platformer.**