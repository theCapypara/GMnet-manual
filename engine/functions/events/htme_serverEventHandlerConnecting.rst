``htme_serverEventHandlerConnecting(script)``
---------------------------------------------

Description
~~~~~~~~~~~

Call a script if a new player connected. This script has to meet the
following specifications:

Callback Arguments:
^^^^^^^^^^^^^^^^^^^

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| playe | ds\_m | a ds\_map    |
| r\_ma | ap    | with the     |
| p     |       | keys ip and  |
|       |       | port, which  |
|       |       | contain ip   |
|       |       | and port of  |
|       |       | the player   |
+-------+-------+--------------+

Callback Returns:
^^^^^^^^^^^^^^^^^

| TRUE if the connection is accepted. The engine will then register the
  player
| FALSE if the connection should be refused, the server will abort
  connection

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
|       | a     | connected.   |
|       | scrip |              |
|       | t     |              |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
