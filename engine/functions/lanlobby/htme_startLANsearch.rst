``tme_startLANsearch(port,[gamefilter])``
-----------------------------------------

Description
~~~~~~~~~~~

**Detailed information in `Tutorial - Bonus 3 - A LAN
lobby <tutorial/15_lanlobby>`__.**

Search in the LAN for servers on the port specified. You can now use
**htme\_getLANServers()** to get a list of LAN servers. This list will
be filled with servers over time. Run this comamnd again to empty it and
resend the broadcast (to refresh the list).

::

    Format of the list returned by **htme_getLANServers()**:
    ds_list:
     [0...] => ds_map:
               [ip]    => string
               [port]  => real
               [data1] => string
               [data2] => string
               [data3] => string
               [data4] => string
               [data5] => string
               [data6] => string
               [data7] => string
               [data8] => string

Arguments
~~~~~~~~~

+-------+-------+--------------+
| Name  | type  | description  |
+=======+=======+==============+
| limit | real  | The port to  |
|       |       | scan on      |
+-------+-------+--------------+
| [game | strin | Only list    |
| filte | g     | servers that |
| r]    |       | match this   |
|       |       | excact       |
|       |       | string for   |
|       |       | their first  |
|       |       | data string  |
|       |       | (the         |
|       |       | gamename).   |
|       |       | Can be EMPTY |
|       |       | STRING if    |
|       |       | you don't    |
|       |       | want to      |
|       |       | filter       |
+-------+-------+--------------+

Returns
~~~~~~~

Nothing
