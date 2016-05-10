VarGroup SyncTypes (mp\_type)
-----------------------------

Each `Variable Group <concepts/vargroups>`__ can be assigned one
syncType using `mp\_setType <functions/sync/mp_setType>`__ that controls
how the varGroup will be synchonized. They are enum values of the enum
``mp_type``. FAST actually means ``mp_type.FAST``! The default value, if
you don't use mp\_setType, is ``mp_type.FAST``.

These are your options:

-  **FAST**: The engine sends the variable **once** in the interval you
   set. Since we are using UDP for networking, there is no assurance,
   that it will actually arrive. That means we don't know if the other
   players actually get this change. The packet could get lost. However,
   using FAST is very fast.
-  **IMPORTANT**: When using IMPORTANT, the variable will still be
   synced in the set interval. However, we are using a special way in
   *GMnet ENGINE* to make sure the packet arrives. Every X seconds, the
   server/client will flood the other players with the information,
   until they respond back, that they got it. That's how we assure the
   information is actually sent. This is however a pretty traffic heavy
   operation and using that in too short intervals will cause lagg in
   both connection and framerate.
-  **SMART**: This is like IMPORTANT but better. Instead of syncing
   every X seconds, we will only sync every X seconds what has changed.
   This is basicly a more traffic-friendly version of IMPORTANT.
