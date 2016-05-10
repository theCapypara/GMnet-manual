Variable Groups
---------------

**Variable Groups** or **VarGroups** describe a group of variables of an
instance that are synced via the engine.

Create a new VarGroup:
~~~~~~~~~~~~~~~~~~~~~~

-  `**mp\_add**\ (groupname,variables,datatype,interval); <functions/sync/mp_add>`__
-  `**mp\_addPosition**\ (groupname,interval); <functions/sync/mp_addPosition>`__
-  `**mp\_addBuiltinBasic**\ (groupname,interval); <functions/sync/mp_addBuiltinBasic>`__
-  `**mp\_addBuiltinPhysics**\ (groupname,interval); <functions/sync/mp_addBuiltinPhysics>`__

Change the `SyncType <concepts/synctypes>`__ of the group:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  `**mp\_setType**\ (groupname,syncType); <functions/sync/mp_setType>`__

Give the group a `Tolerance <concepts/tolerance>`__:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  `**mp\_tolerance**\ (groupname,tolerance); <functions/sync/mp_tolerance>`__
