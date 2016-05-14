Delta time and room_speed
-------------------------

The engine can use ``room_speed`` (default) or delta time.

room_speed
~~~~~~~~~~
The engine is set to use ``room_speed`` as the default timer count.
You use it when you sync objects:

.. code-block:: gml

    mp_addPosition("Pos",5*room_speed);
    mp_add("playerName","name",buffer_string,60*room_speed);

In htme_config:

.. code-block:: gml

    self.udphp_rctintv = 3*60*room_speed;
    self.global_timeout = 5*room_speed;
    self.punch_stage_timeout=1*room_speed;
    self.lan_interval = 15*room_speed;

Room speed is simple to use, understand and works most of the time.

room_speed limits
~~~~~~~~~~~~~~~~~

Game Lag

If your game experience lag the
room halt and so do the room speed count. Lets say that you are connected to a server and your game lag for 3 seconds. Note that the ``global_timeout``
is set to ``5*room_speed`` = 5 seconds. You and the server got each a counter running. And these counters is not synchronized. Server counter can be on 3 and yours on 1.
This means that your game will disconnect if the server don't respond within 5 seconds.
But it also means that the server will kick you if you don't send anything within 5 seconds.
The server got his eyes on his watch and if your lag is on his 3 second count you will be kicked.
Because 3+3 lag=6 seconds.

Different room speeds

Another issue is that your game must have the same room speed in all rooms. Because if you are in a room with speed 30.
And the server is in a room with speed 60. Every second for you is 2 seconds for the server. So you will be kicked.
Because 3*2=6. So after 3 seconds on your counter the server will be on 6 and kick you. 

Delta time
~~~~~~~~~~
Delta time can compensate for lag and different room speed. Because it counts real seconds. If your game lag for 3 seconds.
The counter is still counting.

Delta time setup
~~~~~~~~~~~~~~~~
You need to setup the engine to use delta time. This means that all timers must be changed to real seconds.
When using room speed you set:

.. code-block:: gml

    mp_addPosition("Pos",5*room_speed);

But you need to change it to:

.. code-block:: gml

    mp_addPosition("Pos",5);

This set the time to 5 seconds.
**Note: Sometimes you set the time just to 3 to update the position every 3 steps. 
But if you activate delta time this means 3 seconds now. 
So say your room speed is 30 you must change it to 0.1. Because 3 steps in a room with room_speed 30 is 0.1 seconds.**

But we need to set this up. First go to the script ``htme_config``and set:

.. code-block:: gml

    use_delta_time=true;

You also need to remove all the ``room_speed`` in ``htme_config``.

.. code-block:: gml

    self.udphp_rctintv = 3*60;
    self.global_timeout = 5;
    self.punch_stage_timeout=1;
    self.lan_interval = 15;

And go throught all your synced object and remove the ``room_speed``.

.. code-block:: gml

    mp_addPosition("Pos",5);
    mp_add("playerName","name",buffer_string,60);