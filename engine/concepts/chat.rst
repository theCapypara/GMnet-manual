CHAT Interface
--------------

The CHAT (Custom Handler for Advanced Traffic) Interface is a new way of
syncing information between players.

Instead of using objects and instances, this uses a more classic
approach. Using the CHAT Interface you can send and retrieve string
messages, with the support for multiple channel.

CHAT messages are sent using the **IMPORTANT** `sync
type <concepts/synctypes>`__.

Tutorial
~~~~~~~~

-  `Creating a chat system with it <tutorial/11_chat>`__
-  `Call scripts over the network using the CHAT Interface
   (RPC) <tutorial/17_rpc>`__

Commands
~~~~~~~~

-  `mp\_syncAsChatHandler <./functions/chat/mp_syncAsChatHandler>`__ for
   registering an object to recieve and send messages on a channel.
-  `mp\_chatGetQueue <./functions/chat/mp_chatGetQueue>`__ to recieve
   new messages.
-  `mp\_chatSend <./functions/chat/mp_chatSend>`__ to send messages.
-  `htme\_chatGetMessage <./functions/chat/htme_chatGetMessage>`__ to
   get the message out of a message.
-  `htme\_chatGetSender <./functions/chat/htme_chatGetSender>`__ to get
   the author of a message.
