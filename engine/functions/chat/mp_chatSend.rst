``mp_chatSend(message,[to])``
-----------------------------

Description
~~~~~~~~~~~

Object has to be set up with
`mp\_syncAsChatHandler <functions/chat/mp_syncAsChatHandler>`__ first,
otherwise an error will occur.

Send message via the CHAT Interface over this chanel. The message has to
be a string. You can also experiment with json to send more complicated
data.

This message will by default be sent to all clients and the server [also
the local game!] and can be retrieved via
`mp\_chatGetQueue <functions/chat/mp_chatGetQueue>`__.

Use the additional 'to' argument to only send this message to one
player.

Example
~~~~~~~

Read the tutorial `about creating a chat system <tutorial/11_chat>`__
for more information.

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| messa | strin | The message  |
| ge    | g     | to send      |
+-------+-------+--------------+
| [to]  | strin | (optional;   |
|       | g     | Will send to |
|       |       | all by       |
|       |       | default)     |
|       |       | hash of the  |
|       |       | player that  |
|       |       | the message  |
|       |       | should be    |
|       |       | sent to.     |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
