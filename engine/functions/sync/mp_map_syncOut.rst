``mp_map_syncOut(varName, variable)``
-------------------------------------

Description
~~~~~~~~~~~

More information: `mp\_map\_syncIn and
mp\_map\_syncOut <concepts/instancevars>`__

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| varNa | strin | Name of the  |
| me    | g     | variable to  |
|       |       | get          |
+-------+-------+--------------+
| varia | any   | Value of the |
| ble   |       | variable     |
|       |       | that the     |
|       |       | instance     |
|       |       | currently    |
|       |       | has. Will    |
|       |       | later be     |
|       |       | used to      |
|       |       | compare them |
|       |       | to values in |
|       |       | the engine.  |
|       |       | Currently    |
|       |       | this is      |
|       |       | returned if  |
|       |       | the engine   |
|       |       | has no valid |
|       |       | data for     |
|       |       | this         |
|       |       | varName.     |
+-------+-------+--------------+

Returns
~~~~~~~

Value of varName in the variable map of this instance
