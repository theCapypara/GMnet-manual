``mp_chatGetQueue()``
---------------------

Description
~~~~~~~~~~~

Object has to be set up with mp\_syncAsChatHandler first, otherwise an
error will occur.

Get a ds\_queue containing all not processed string that recieved via
this channel. All entries in this queue can be decoded using these
commands: \* `htme\_chatGetSender <functions/chat/htme_chatGetSender>`__
- To get the playerhash of the player that sent this message \*
`htme\_chatGetMessage <functions/chat/htme_chatGetMessage>`__ - To get
the chat message.

Example
~~~~~~~

Read the tutorial `about creating a chat system <tutorial/11_chat>`__
for more information.

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

A ds\_queue, it's entries can be decoded using the functions above.
