``udphp_downloadServerList(...)``
---------------------------------

Description
~~~~~~~~~~~

**Detailed information in `Tutorial - Bonus 1 - An ONLINE
lobby <tutorial/13_lobby>`__.**

Download the list of servers from the master server.

global.udphp\_downloadlist\_refreshing will be set true. It will be set
false again if download is finished and **global.udphp\_downloadlist**
will contain a list of online servers then. If download fails,
global.udphp\_downloadlist\_refreshing will never reset. It will fail,
if the master server has the lobby disabled or is not reachable.

Use the (optional) arguments to sort and filter the list. Default
sorting can be seen below under arguments.

Format of **global.udphp\_downloadlist**:

::

    ds_list:
     [0...] => ds_map:
               [ip]    => string
               [data1] => string
               [data2] => string
               [data3] => string
               [data4] => string
               [data5] => string
               [data6] => string
               [data7] => string
               [data8] => string
               [createdTime] => string -> can be converted to real
                                unix timestamp, time the server was created.

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| [limi | strin | The number   |
| t]    | g/rea | of servers   |
|       | l     | to return or |
|       |       | EMPTY STRING |
|       |       | if ALL       |
|       |       | servers      |
|       |       | should be    |
|       |       | returned     |
|       |       | (optional)   |
+-------+-------+--------------+
| [sort | strin | Field to     |
| by]   | g     | sort the     |
|       |       | result by,   |
|       |       | this can be: |
|       |       | date (filter |
|       |       | by time      |
|       |       | created;     |
|       |       | DEFAULT),    |
|       |       | data1,       |
|       |       | data2,       |
|       |       | data3,       |
|       |       | data4,       |
|       |       | data5,       |
|       |       | data6,       |
|       |       | data7, data8 |
|       |       | (optional)   |
+-------+-------+--------------+
| [sort | strin | Sort         |
| by\_d | g     | ascending    |
| ir]   |       | ("ASC") or   |
|       |       | descending   |
|       |       | ("DESC";     |
|       |       | DEFAULT)     |
|       |       | (optional)   |
+-------+-------+--------------+
| [filt | strin | Only list    |
| er\_d | g     | servers that |
| ata1] |       | match this   |
|       |       | excact       |
|       |       | string for   |
|       |       | their first  |
|       |       | data string  |
|       |       | (the game    |
|       |       | name). Can   |
|       |       | be EMPTY     |
|       |       | STRING if    |
|       |       | you don't    |
|       |       | want to      |
|       |       | filter       |
|       |       | (optional)   |
+-------+-------+--------------+
| [filt | strin | See above;   |
| er\_d | g     | but for      |
| ata2] |       | second data  |
|       |       | string       |
|       |       | (optional)   |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata3] |       |              |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata4] |       |              |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata5] |       |              |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata6] |       |              |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata7] |       |              |
+-------+-------+--------------+
| [filt | strin | See above... |
| er\_d | g     | (optional)   |
| ata8] |       |              |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
