``mp_setType(group,type)``
--------------------------

Description
~~~~~~~~~~~

Changes the type with which a group will be synced to the other clients.

More information: `VarGroup SyncTypes (mp\_type) <concepts/synctypes>`__

Example
~~~~~~~

.. code-block:: gml

    ///Create Event
    mp_sync();
    mp_addBuiltinPhysics("physics",10*room_speed);
    mp_setType("physics",mp_type.SMART);

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| group | strin | The name of  |
| name  | g     | the group of |
|       |       | which you    |
|       |       | want to      |
|       |       | change the   |
|       |       | type of      |
+-------+-------+--------------+
| inter | real  | The values   |
| val   |       | of the enum  |
|       |       | mp\_type can |
|       |       | be seen in   |
|       |       | htme\_config |
|       |       | or `the      |
|       |       | manual <conc |
|       |       | epts/synctyp |
|       |       | es>`__.      |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
