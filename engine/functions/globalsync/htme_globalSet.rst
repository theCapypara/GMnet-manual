``htme_globalSet(name,value,datatype)``
---------------------------------------

Description
~~~~~~~~~~~

Stores a real or string value in the global sync list. Use buffer\_type
to define the type of the variable. The global sync list is a list of
global variables that can be retrived via htme\_globalGet.

They get synced between all clients and servers and be read and written
by any (unlike instance variables which are read-only for all but the
creator).

Make sure the player is connected or a server is running!

**NOTE:** Using this command will sync this variable immediately via
`SMART <concepts/synctypes>`__

More information: `Bonus 2 - Global Sync (Sync a pool of variables
editable by all) <tutorial/14_globalsync>`__

Example
~~~~~~~

.. code-block:: gml

    var value = 1+1;
    htme_globalSet("name",value,buffer_u8);

Arguments
~~~~~~~~~

+------------+---------------+-----------------------------------------------------+
| Name       | type          | description                                         |
+============+===============+=====================================================+
| name       | string        | The name of the variable                            |
+------------+---------------+-----------------------------------------------------+
| value      | real/string   | The (new) value of the variable you want to store   |
+------------+---------------+-----------------------------------------------------+
| datatype   | real          | See `Buffer type <concepts/buffer>`__               |
+------------+---------------+-----------------------------------------------------+

Returns
~~~~~~~

Nothing
