States of the engine
--------------------

The engine can be in different states.

1. Is the engine running (=Server or Client started)? ->
   `htme\_isStarted <functions/tools/htme_isStarted>`__ returns true
2. Are we running the server? ->
   `htme\_isServer <functions/tools/htme_isServer>`__ returns true
3. (Only client) -> Is the client connected to a server? ->
   `htme\_clientIsConnected <functions/tools/htme_clientIsConnected>`__
   returns true
4. (Only client) -> Did a connection to the server fail? ->
   `htme\_clientConnectionFailed <functions/tools/htme_clientConnectionFailed>`__
   returns true
