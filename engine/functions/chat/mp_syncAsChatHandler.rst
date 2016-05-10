``mp_syncAsChatHandler(channel)``
---------------------------------

Description
~~~~~~~~~~~

Add this object as a handler for traffic via the CHAT Interface.

This object can then send and recieve traffic on the specified channel
using `mp\_chatGetQueue <functions/chat/mp_chatGetQueue>`__ and
`mp\_chatSend <functions/chat/mp_chatSend>`__.

This is independent from mp\_sync and it's mp commands. You don't have
to use mp\_sync.

Example
~~~~~~~

Read the tutorial `about creating a chat system <tutorial/11_chat>`__
for more information.

Arguments
~~~~~~~~~

+-----------+----------+----------------------------------------------------+
| Name      | type     | description                                        |
+===========+==========+====================================================+
| channel   | string   | The name of the channel to assign to this object   |
+-----------+----------+----------------------------------------------------+

Returns
~~~~~~~

Nothing
