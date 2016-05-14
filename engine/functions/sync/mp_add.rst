``mp_add(groupname,variables,datatype,interval)``
-------------------------------------------------

Description
~~~~~~~~~~~

Adds a new `group of variables <concepts/vargroups>`__ to be synced to
this instance.

Please read this manual page when using mp\_add: `mp\_map\_syncIn and
mp\_map\_syncOut <concepts/instancevars>`__

Example
~~~~~~~

.. code-block:: gml

    ///Create Event
    mp_sync();
    mp_add("playerName","name",buffer_string,10*room_speed);;

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
| varia | strin | A list of     |
| bles  | g     | local         |
|       |       | variables of  |
|       |       | the instance  |
|       |       | seperated     |
|       |       | with commas   |
+-------+-------+---------------+
| datat | real, | A value of a  |
| ype   | buffe | "buffer\_"    |
|       | r\_\* | constant to   |
|       |       | specify the   |
|       |       | data type of  |
|       |       | all           |
|       |       | variables in  |
|       |       | this group.   |
|       |       | `See manual`_ |
|       |       | for a list    |
|       |       | of datatypes  |
|       |       | and their     |
|       |       | meanings.     |
|       |       | All           |
|       |       | datatypes     |
|       |       | from enum     |
|       |       | mp\_buffer\_  |
|       |       | types         |
|       |       | are also      |
|       |       | allowed but   |
|       |       | should not    |
|       |       | be used by    |
|       |       | you as a      |
|       |       | user!         |
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
.. _See manual:  concepts/buffer