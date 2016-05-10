``htme_clientConnectionFailed()``
---------------------------------

Description
~~~~~~~~~~~

Check if the client did not manage to connect in time. Only call this
after creating a client, otherwise the result will be invalid.

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

True if the engine is operating in client mode and gave up to connect.
