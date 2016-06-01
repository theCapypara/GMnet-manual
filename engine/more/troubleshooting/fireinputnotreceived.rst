Fire input not received on client
---------------------------------

Sometimes you may experience that some keytrokes is missing on the client side. Ex say you use this code:

Create event:

.. code-block:: gml

    self.firenow=false;
    mp_add("firebutton","firenow",buffer_bool,1);

Step Begin event:

.. code-block:: gml

    if (htme_isLocal())
    {
        self.firenow= keyboard_check_pressed(vk_space);
    }

    mp_map_syncIn("firenow",self.firenow);

Step End event:

.. code-block:: gml

    self.firenow=mp_map_syncOut("firenow",self.firenow);

This code send a network message to the other players every step.
But sometime the client wont receive the message.
This is because of network lag.

You send 30 network messages per sec. These messages is sent to the client. 
But every message take about 10-600 milliseconds to reach the other player.
This means that some of the messages may be bundled and be received at the same time.
Say you press fire 2 times within 1 sec. Under 1 sec the messages look like this. 
Every 0 is a no fire and 1 is a fire. Ever space is a step in gm. You send a perfect array of messages.
0 0 0 0 0 0 0 0 0 1
0 0 0 0 0 0 0 0 0 1
0 0 0 0 0 0 0 0 0 0
But the player who receives the messages may receive them like this
000 0000001
00 0000 000100
00000000
The other player received several messages in the same step. 000 is ok. 
0000001 is ok because the 1 was the last message received in this step and ``self.firenow`` will be true when the step event run in the player. 
00 and 0000 ok. But here it comes. 000100 here the other player receive 6 messages in the same step. 
Even if 1 fire was in there the last message received set ``self.firenow`` to false. So no fire this step.

Send only when needed
~~~~~~~~~~~~~~~~~~~~~

You can fix this by increasing the ``mp_add("firebutton","firenow",buffer_bool,room_speed*100);``
This will stop to send messages every step. But when you fire you need to send it. 
You can do this by calling ``htme_syncGroupNow("firebutton")``.

if htme_isLocal()
{
    If keyboard_check_pressed(ord("f"))
    {
        firenow=true
        mp_map_syncIn("firenow",self.firenow);
        htme_syncGroupNow("firebutton");
    }
    Else if keyboard_check_released(ord("f"))
    {
        firenow=false
        mp_map_syncIn("firenow",self.firenow);
        htme_syncGroupNow("firebutton");
    }
}