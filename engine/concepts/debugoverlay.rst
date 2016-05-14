The debug overlay
-----------------

The debug overlay is a new feature that allows you to do better
debugging. Enable it by setting ``self.debugoverlay`` to true in
**htme\_config**.

.. raw:: html

   <iframe width="420" height="315" src="https://www.youtube.com/embed/JsEMMpaFg9c" frameborder="0" allowfullscreen>

.. raw:: html

   </iframe>

F12: Toggle overlay
-------------------

F12 will show and hide the overlay when it's enabled.

F1: All instances
-----------------

Shows a list of all instances and the `variable
groups <concepts/vargroups>`__ for `local
instances <concepts/instances>`__.

For the first 10 instances in the list, press SHIFT + the shown number
to access instance details.

Instance details
~~~~~~~~~~~~~~~~

+-----------+-----------+
| Variable  | Descripti |
|           | on        |
+===========+===========+
| Hash      | The id of |
|           | the       |
|           | instance  |
|           | as stored |
|           | by the    |
|           | engine    |
+-----------+-----------+
| isVisible | Whether   |
|           | or not    |
|           | this is a |
|           | visible   |
|           | instance  |
+-----------+-----------+
| isNotCach | True if   |
| ed        | this      |
|           | instance  |
|           | is in the |
|           | same room |
|           | (server   |
|           | only;     |
|           | clients   |
|           | will only |
|           | show      |
|           | instances |
|           | in the    |
|           | same      |
|           | room)     |
+-----------+-----------+
| Persisten | See       |
| t         | `Instance |
|           | scrope    |
|           | and       |
|           | rooms <co |
|           | ncepts/sc |
|           | ope>`__   |
+-----------+-----------+
| stayAlive | See       |
|           | `Instance |
|           | scrope    |
|           | and       |
|           | rooms <co |
|           | ncepts/sc |
|           | ope>`__   |
+-----------+-----------+
| Instance  | The local |
| ID        | id of the |
|           | instance, |
|           | assgined  |
|           | by        |
|           | GameMaker |
|           | .         |
|           | If cached |
|           | the       |
|           | instance  |
|           | will not  |
|           | actually  |
|           | exist,    |
|           | and       |
|           | therefor  |
|           | the       |
|           | instance  |
|           | will have |
|           | no id     |
+-----------+-----------+
| Object    | Name of   |
|           | the       |
|           | object of |
|           | this      |
|           | instance  |
+-----------+-----------+
| Player    | Number    |
|           | and hash  |
|           | of the    |
|           | player    |
|           | this      |
|           | instance  |
|           | belongs   |
|           | to        |
+-----------+-----------+
| Saved     | All       |
| variables | variables |
|           | as synced |
|           | by the    |
|           | engine    |
+-----------+-----------+
| Vargroups | Details   |
|           | of all    |
|           | `variable |
|           | groups <c |
|           | oncepts/v |
|           | argroups> |
|           | `__       |
+-----------+-----------+

F2: Visible instances
---------------------

Same as F1 but filters by showing only visible instances

F3: Players
-----------

Shows a list of all players, including their player number and their
hash. Also shows who is the local player and who runs the server.

Press SHIFT + number shown to show all instances of one player. If you
are the server, press STRG + number to kick a player.

F4: Invisible instances
-----------------------

Same as F1 but filters by showing only invisible instances

F5: Instances in cache
----------------------

Same as F1 but showing only cached instances (instances in same room;
This list is always empty for clients).

F6: Global sync
---------------

Shows all variables in the global sync pool.

F7: CHAT Interface Channels
---------------------------

Lists all `CHAT Interface <./concepts/chat>`__ channels and how many
messages haven't been processed (read) and what the content of the most
recent unread message is.

F8: Signed packet queue
-----------------------

Shows details about all `signed packets <concepts/signedpackets>`__ that
are not yet recieved by the clients/server.

F9-F10
------

*Not implemented yet*.

F11: Disconnect - Client only
-----------------------------

Disconnect from the server. This will tell the server to kick us and
then kill the engine.

Check if overlay is enabled
---------------------------

``htme_debugOverlayEnabled`` will return true when the overlay is
enabled. Use this to draw your own debug stuff when the overlay is
active.
