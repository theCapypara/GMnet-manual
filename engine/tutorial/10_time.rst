Adding day and night
--------------------

Now we want to add time and a day and night cycle. Obviously we want to
sync the time between all players.

So let's just create a new object, I guess?

...But wait. If we simply sync a time object using the engine, we will
end up having one time object per player. For 4 players that means we
would have four time objects fighting over each other.

Of course we could tell all objects to only increase the time when it's
locally, but then they would all have their own time counter and that
would have the same effect of not syncing them at all.

**Oh, if there would only be an easy way to fix this...
Oh! Wait! There is!**

You can check if the object was **created on the server** with
``htme_isServer()``. This way you can\*\* add objects that get
controlled by the server and synced to each player\*\*. You have 1
instance on 4 PCs, instead of 4 instances at 4 PCs.

Let me show you how this works.

**Create a new object** called ``htme_obj_time``. Add the following code
to the beginning of the create event:

.. code-block:: gml

    if (!htme_isServer()) {
       instance_destroy();
       exit;
    }

| Let's prevent **I'm a client**:
| I create the instance, **see that I'm not the server**, instantly
  **destroy it** and then **recieve the instance from the server
  controlled by the server**.

Genius!

After that bit of code we add the code to add our new object to the
engine, which is of course never executed when created clientside:

.. code-block:: gml

    mp_sync();
    mp_add("time","time",buffer_u16,20*room_speed);
    mp_setType("time",mp_type.SMART);
    //And at the end we set the time to 1000 - this will be noon
    self.time = 1000;

This way the\*\* clients recieve the time every 20 seconds\ **. We are
going to program the counter so, that it counts up, even clientside.
That means **\ each player's game counts up on their own\ **, and the
server **\ corrects the time if neccessary\*\*.

**Because we used ``mp_add``** we need to add the following code to
**begin step**:

.. code-block:: gml

    mp_map_syncIn("time",self.time);

And this to **end step**

.. code-block:: gml

    self.time = mp_map_syncOut("time", self.time);

The two things left are counting the time up and actually doing
something with it.

Increasing the time
~~~~~~~~~~~~~~~~~~~

Remember that, because we use ``mp_add``, all changes to our ``time``
variable need to be made before ``mp_map_syncIn`` is called. Because of
that, create a new code block in **position 1 of begin step**:

.. code-block:: gml

    ///Increase the time. If time is greater than 2000, set to zero.
    self.time++;
    if (self.time > 2000) self.time = 0;

This will count up our time to 2000 which is midnight, and then reset it
to 0, which is also midnight. 1000 is noon.

If you want to perform actions on these server controlled instances only
by the server use ``if (htme_isLocal()) {}``. Everything inside this
statement will only be executed by the server.

Day and night
~~~~~~~~~~~~~

Paste the following code into the **Draw-Event**. This will change the
background color in the first room depending on time and display the
time. Room 2 will be interior.

.. code-block:: gml

    ///Draw background
    if (room == htme_rom_demo) {
        //Draw night/day
        //This is not a good way of doing it, but I'm not in the mood for that :D
        if (self.time == 0) {
           var bgcolor = make_colour_hsv(170,185,0);
        } else if (self.time <= 1000) {
           var bgcolor = make_colour_hsv(170,185,255/100*(self.time)/10);
        } else if (self.time == 1001) {
           var bgcolor = make_colour_hsv(170,185,255);
        } else if (self.time <= 2000) {
           var bgcolor = make_colour_hsv(170,185,255/100*(1000-self.time)/10);
        }
        draw_set_colour(bgcolor);
        draw_rectangle(0,0,room_width,room_height,false);
        //Draw time as debug on screen
        draw_set_colour(c_white);
        draw_text(room_height-70,70,"Time: "+string(self.time));
    } else {
      draw_set_colour(c_maroon);
      draw_rectangle(0,0,room_width,room_height,false);
    }
    draw_set_colour(c_white);

That's not right...
~~~~~~~~~~~~~~~~~~~

Now when testing what we just did, you might realize that **it doesn't
work right**. **Even** if you set ``htme_obj_time`` to be
**persistent**, the time object **just vanishes sometimes**. Let's take
a look again at our nice table again:

.. figure:: images/2v2.PNG
   :alt: The nice table

   The nice table

As you can see in this table, **if the server is A and A is in Room 2,
the time object will simply disappear on all clients**. Or if the server
is in Room 1 and the client(s) in Room 2. And if you don't even set it
to be persistent, it even disappears for the server if he is in Room 2.
A nightmare!

That's not good! We want our new time object to allways exist, no matter
what!

So, first, **set ``htme_obj_time`` to be persistent**. Now,\*\* after
the ``mp_sync();`` in the create event\*\* add this:

.. code-block:: gml

    mp_stayAlive();

This tells the engine to **keep this instance alive, no matter what**.
This ONLY works if the object is persistent!

When we add this to our table, things look like this:

.. figure:: images/4.PNG
   :alt: The even nicer table

   The even nicer table

As you can see, with stayAlive enabled, the instance always exists.

Done!
~~~~~

Time and day is done. Test it out!

We are now ready for the final chapter...: A chat system...