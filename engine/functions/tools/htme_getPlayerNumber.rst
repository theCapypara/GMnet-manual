``htme_getPlayerNumber(playerhash)``
------------------------------------

Description
~~~~~~~~~~~

Extracts the number of the player from the playerhash The number starts
at 1 for the server, 2 is the first connected client, 3 the third and so
on. If 2 disconnects, the next player connecting will occupy place 2
again.

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| playe | strin | A playerhash |
| rhash | g     | as stored in |
|       |       | the list     |
|       |       | that you can |
|       |       | get with     |
|       |       | htme\_getPla |
|       |       | yers.        |
+-------+-------+--------------+

Returns
~~~~~~~

The player number
