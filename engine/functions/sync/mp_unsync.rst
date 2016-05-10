``mp_unsync()``
---------------

Description
~~~~~~~~~~~

Removes an instance from the engine and \* if not
[local]concepts/instances): destroys it [DO NOT USE IT ON REMOTE
INSTANCES!] \* if local: informs server which then informs all players.

Does NOT destroy local instances! You have to do that yourself when
calling this manually!

Example
~~~~~~~

.. code-block:: gml

    ///Step
    if (somethinghappend && htme_isLocal()) {
        mp_unsync();
        instance_destroy();
    }

Arguments
~~~~~~~~~

None

Returns
~~~~~~~

Nothing
