``htme_chatGetSender(chat_queue_entry)``
----------------------------------------

Description
~~~~~~~~~~~

Get the sender of a CHAT Interface message. See
`mp\_chatGetQueue <functions/chat/mp_chatGetQueue>`__ for details.

Example
~~~~~~~

Read the tutorial `about creating a chat system <tutorial/11_chat>`__
for more information.

Arguments
~~~~~~~~~

+----------------------+----------+--------------------------------------------------------------------------------------------+
| Name                 | type     | description                                                                                |
+======================+==========+============================================================================================+
| chat\_queue\_entry   | string   | An entry of the queue returned by `mp\_chatGetQueue <functions/chat/mp_chatGetQueue>`__.   |
+----------------------+----------+--------------------------------------------------------------------------------------------+

Returns
~~~~~~~

Playerhash of the player that sent this message
