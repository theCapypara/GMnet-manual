``htme_globalGet(name)``
------------------------

Description
~~~~~~~~~~~

Returns a variable from the global sync list. See htme\_globalSet for
information on what these variables are. Will return undefined if
variables was not stored previously by any client or the server. Make
sure the player is connected or a server is running!

More information: `Bonus 2 - Global Sync (Sync a pool of variables
editable by all) <tutorial/14_globalsync>`__

Example
~~~~~~~

.. code-block:: gml

    var value = htme_globalGet("name")

    if (is_undefined(value) {
        //Nope, that wasn't set yet...
    }

Arguments
~~~~~~~~~

+--------+----------+----------------------------+
| Name   | type     | description                |
+========+==========+============================+
| name   | string   | The name of the variable   |
+--------+----------+----------------------------+

Returns
~~~~~~~

The saved variable (real or string) or undefined
