``htme_isLostConnection()``
--------------------

Description
~~~~~~~~~~~

Check if the connection is lost. This will also clean the engine and you can go to the main room if the script return true.

.. code-block:: gml

    if htme_isLostConnection()
    {
        room_goto(rm_main);
    }

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

True if the connection is lost.
