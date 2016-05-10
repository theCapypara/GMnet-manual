mp\_map\_syncIn and mp\_map\_syncOut
------------------------------------

Whenever you use `mp\_add <functions/sync/mp_add>`__, you need to do 2
things for each variable you sync with it:

1. Add the following to the end step event:
   ``gml    self.VARIABLENAME = mp_map_syncOut("VARIABLENAME", self.VARIABLENAME);``
   Where you replace "VARIABLENAME" with the name of your variable.

2. Run the following code whenever you change that variable, we
   recommend doing this in the begin step event:
   ``gml    mp_map_syncIn("VARIABLENAME",self.VARIABLENAME);`` This also
   needs to be done at least once after you set up the engine if you
   don't put it in begin step.

**THIS DOES NOT TO BE DONE FOR ANY OTHER FUNCTION STARTING WITH mp\_add.
ONLY WITH mp\_add ITSELF!**

Technical explanation
~~~~~~~~~~~~~~~~~~~~~

The engine needs to know what variables it needs to sync. So if you
execute this code:

.. code-block:: gml

    mp_add("message","message",buffer_string,5);

Then we know you want to sync the variable message. The
problem/limitation in Game Maker is, that we can't get the value of the
message variable of this instance now. Why?

Well let me have an example. This works:

.. code-block:: gml

    var instance; //Some valid instance
    var test = (instance).x;
    //Test will now have the x position of the instance as value

Now in that case we are directly accessing the x-Position of the
instance. That's what all other mp\_add\* functions besides mp\_add
itself do, because they can be hardcoded. When writing the code we
already know what to sync and in what order.

We don't know how your variables are called while coding, so we have to
get them dynamically. Let's take the following exmaple:

.. code-block:: gml

    var instance; //Some valid instance
    var variable = "x";
    //What now???
    var test = (instance).variable; //? Doesn't work!
    var test = (instance).(variable); //? Doesn't work!
    var test = (instance)[variable]; //? Doesn't work!

There's no way in Game Maker Studio of doing that. That's why we use a
ds\_map to cache your instances variables. Because with a ds\_map, that
does work!

.. code-block:: gml

    var map; //Some valid ds_map that belongs to your instance; That's what you change when using the syncIn and syncOut command
    var variable = "x";

    var test = ds_map_find_value(map,variable); //Yay! Works!
