``htme_isServer()``
-------------------

Description
~~~~~~~~~~~

Check if this engine is running in server mode.

**NOTE:** This will always return true when called by `non local
instances <concepts/instances>`__, this can't be used to identify if a
remote instance belongs to the server!

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

True if running in server mode, except when called by a remote instance,
in that case it will always return true.
