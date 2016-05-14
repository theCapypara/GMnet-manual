``mp_addPosition(groupname,interval)``
--------------------------------------

Description
~~~~~~~~~~~

Adds a new group of variables to be synced to this instance.

The variables are: \* x,y

Example
~~~~~~~

.. code-block:: gml

    ///Create Event
    mp_sync();
    mp_addPosition("pos",10*room_speed);;

Arguments
~~~~~~~~~

+-------+-------+---------------+
| Name  | type  | description   |
+=======+=======+===============+
| group | strin | The name of   |
| name  | g     | the group,    |
|       |       | this is only  |
|       |       | used locally  |
|       |       | to identify   |
|       |       | this group,   |
|       |       | for example   |
|       |       | if you want   |
|       |       | to use        |
|       |       | `mp_setType`_ |
+-------+-------+---------------+
| inter | real  | The interval  |
| val   |       | in which the  |
|       |       | variable      |
|       |       | group get's   |
|       |       | synced with   |
|       |       | the other     |
|       |       | players       |
+-------+-------+---------------+

Returns
~~~~~~~

Nothing

.. _mp_setType:  functions/sync/mp_setType