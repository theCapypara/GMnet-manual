``htme_serverEventHandlerDisconnecting(script)``
------------------------------------------------

Description
~~~~~~~~~~~

Call a script if a player disconnected. This script has to meet the
following specifications:

Callback Arguments:
^^^^^^^^^^^^^^^^^^^

+---------------+-----------+------------------------------------------------+
| Name          | type      | description                                    |
+===============+===========+================================================+
| player\_map   | ds\_map   | a ds\_map with the keys ip and port and hash   |
+---------------+-----------+------------------------------------------------+

Callback Returns:
^^^^^^^^^^^^^^^^^

Nothing

Example
~~~~~~~

See `BONUS 4 - Event Handlers for
Connecting/Disconnecting <tutorial/16_events>`__.

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| scrip | resso | The script   |
| t     | urce  | to call when |
|       | id of | a player     |
|       | a     | disconnected |
|       | scrip | .            |
|       | t     |              |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
