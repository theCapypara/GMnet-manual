``mp_sync()``
-------------

Description
~~~~~~~~~~~

Configures this instance to be synced via the GMnet ENGINE. This must be
called before all other mp commands.

Example
~~~~~~~

.. code-block:: gml

    ///Create Event
    mp_sync();
    mp_addPosition("Pos",5*room_speed);

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

Nothing
