Chat
----

In this chapter you will learn a new way of syncing information between
players. This method was designed for chat messages and similiar things.

For this we use the so called `CHAT <concepts/chat>`__ (Custom Handler
for Advanced Traffic) Interface. You will learn how to use it in this
chapter and can find more advanced usages of it in chapter `Bonus 5 -
RPC <tutorial/17_rpc>`__.

First, let's **create an object ``htme_obj_chat``**.

We are storing messages in the variable **message**. Or at least **the
last** message sent by a player. Then we are **syncing it** via the
engine, and the **local instance** of that object **will loop through
all chat instances**, like we learned when creating the chat overlay. It
will then **look for new messages in our "inboxes"**, and **add them to
a list that contains all messages**.

Adding a CHAT handler
~~~~~~~~~~~~~~~~~~~~~

Create a **Create-Event** and add the following code:

.. code-block:: gml

    mp_syncAsChatHandler("Chat");

    //Setup variables
    self.output = ds_list_create();

**`mp\_syncAsChatHandler <functions/chat/mp_syncAsChatHandler>`__**.
This function **registers the object to be a sender and reciever for
string messages** for the chanel **Chat**.
*`mp\_sync <functions/chat/mp_sync>`__* is not needed here. We won't be
syncing the object itself, only messages. But you'll see what that means
in a second.

The ds\_list **ouput** is used to **store all chat messages**.

Sending a message.
~~~~~~~~~~~~~~~~~~

We are going to send a message when the player presses the C-key. Create
a **press C-key Event**:

.. code-block:: gml

    self.str_id = get_string_async("Send a chat message:","");

This script uses **``get_string_async``** to **ask the player for the
chat message**. If you never used that before, things might be a bit
complicated, so let me explain:

| ``get_string_async`` displays an input box where the player can input
  text without locking the game, like ``get_string`` would do. That's
  important, because the client or server will loose connection, if the
  game is locked.
| Instead of returning the message, ``get_string_async`` returns a
  number, that we need to store. Inside the **Dialog Event, which can be
  found under Asynchronous** we are retrieving the message:

.. code-block:: gml

    ///Process the message the player typed in
    var i_d = ds_map_find_value(async_load, "id");
    if (i_d == self.str_id) {
       if (ds_map_find_value(async_load, "status")) {
          if (ds_map_find_value(async_load, "result") != "") {
             var message = ds_map_find_value(async_load, "result");
             //Send the message using the CHAT Interface.
             mp_chatSend(message);
          }
       }
    }

This may seem a bit complicated, the code checks that the message
entered was valid, but the important code is the code in the most inner
if-clause.

``var message = ds_map_find_value(async_load, "result");`` retrieves the
message and writes it to the local variable **message**.

Using **`mp\_chatSend(message) <functions/chat/mp_chatSend>`__** we are
now sending this message to all players. It will also be sent to
ourself.

Recieving messages
~~~~~~~~~~~~~~~~~~

Messages are stored in a ds\_queue, which is filled when new messages
arrived. We will be checking every step if new messages arrived.

**In the step event, add the following code**:

.. code-block:: gml

    var queue = mp_chatGetQueue();
    while (ds_queue_size(queue) > 0) {
        var raw_message = ds_queue_dequeue(queue);

The first line uses
`mp\_chatGetQueue <functions/chat/mp_chatGetQueue>`__ to get the queue
of messages and then **we loop through it until it is empty**.
``ds_queue_dequeue`` will **get** the oldest **message** in the queue
and remove it from the queue.

This message however is "encoded", so we now use two functions to decode
it:

.. code-block:: gml

        var sender = htme_chatGetSender(raw_message);
        var message = htme_chatGetMessage(raw_message);

`htme\_chatGetSender <functions/chat/htme_chatGetSender>`__ and
`htme\_chatGetMessage <functions/chat/htme_chatGetMessage>`__ will, as
their name might suggest, return the author of the message (the hash of
the player) and the sended message.

| So now we have the message. What now?
| As you may remember, we gave all our player objects names. **We want
  to display the sent message together with the name of the player**.
| To do that, we first have get the name of the player object using the
  player hash:

.. code-block:: gml

        var player_instance = htme_findPlayerInstance(htme_obj_player,sender);
         if (player_instance != -1) {
             var name = (player_instance).name;
         } else {
             var name = "(Someboy in another room)";
         }

This is the same as in the `chapter 9 <tutorial/9_playerlist>`__, so
check this page of the tutorial for more information.

The last thing we do, is we add the message we recieved to the list we
created in the create event, together with who sent it, seperated by a
":".

.. code-block:: gml

        //Add to list of chat output
        ds_list_add(self.output,name+": "+message);
    }

Display the chat.
~~~~~~~~~~~~~~~~~

To display the chat, put the following code into the **draw-event**:

.. code-block:: gml

    //Get an offset, so we draw the newest line on bottom
    var size = ds_list_size(self.output);
    var bottomLine = room_height-50;
    var offset = size*20;

    for(var i = 0;i<size;i++) {
        var line = ds_list_find_value(self.output,i);
        draw_text(50,bottomLine-offset+i*20,line);
    }

That draw event is not essential part of the engine, so I'm not
explaining it here. It basically loops over the output list and displays
each line.

We are done. Have fun testing it out!

Private messages
~~~~~~~~~~~~~~~~

You can also send private messages to certain players.
`mp\_chatSend <functions/chat/mp_chatSend>`__ supports a second
argument, where you can use the hash of a player to only sent your
messages to specific players. Try it out!