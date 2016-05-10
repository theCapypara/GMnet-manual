GMnet ENGINE Manual: Index
--------------------------

Welcome! Below you will find all pages of this manual. If you are new,
start with the tutorial.

Some sections may have a **PLUS** prefix. These pages are only relevant
if you are using GMnet ENGINE. If you are GMnet CORE or if you disabled
GMnet PUNCH in the settings, these pages do not apply for you. For more
information, check the page on `differences between GMnet CORE and
ENGINE <./versiondifferences>`__

**Note:** GMnet ENGINE was previously called the "HappyTear Multiplayer
Engine" (or HTME for short). This name may be still present on some
pages of the manual, also all scripts and files are prefixed with "HTME"
for this reason. GMnet PUNCH was previously called UDPHP, the same
applies for it.

Tutorial / Getting Started
~~~~~~~~~~~~~~~~~~~~~~~~~~

This tutorial will guide you through the creation of the platformer that
comes with the engine and teaches you how to use the engine. 0. `What is
GMnet ENGINE? <./tutorial/0_whatishtme>`__ 1. `Basic
configuration <./tutorial/1_config>`__ 2. `**PLUS** - Setup GMnet
PUNCH <./tutorial/2_udphp1>`__ 3. `**PLUS** - Hosting a mediation
server <./tutorial/3_udphp2>`__ 4. `Starting the
engine <./tutorial/4_starting>`__ 5. `Setting up the basic
platformer <./tutorial/5_platformer>`__ 6. `The network
controller <./tutorial/6_networkcontroller>`__ 7. `Adding a
player <./tutorial/7_player>`__ 8. `A second room and
doors <./tutorial/8_doors>`__ 9. `Making an overlay that shows the name
of connected players <./tutorial/9_playerlist>`__ 10. `Adding
day/night <./tutorial/10_time>`__ 11. `Creating a chat
system <./tutorial/11_chat>`__ 12. `Conclusion / What's
next <./tutorial/12_end>`__ 13. `**PLUS** - Bonus 1 - ONLINE
lobby <./tutorial/13_lobby>`__ 14. `Bonus 2 - Global Sync (Sync a pool
of variables editable by all) <./tutorial/14_globalsync>`__ 15. `Bonus 3
- LAN lobby <./tutorial/15_lanlobby>`__ 16. `Bonus 4 - Event Handlers
for Connecting/Disconnecting <./tutorial/16_disconnect>`__ 16. `Bonus 5
- RPC <./tutorial/17_rpc>`__

Important Concepts
~~~~~~~~~~~~~~~~~~

-  `Local and remote Instances <./concepts/instances>`__
-  `Instance scope and rooms <./concepts/scope>`__
-  `Players and Playerhashes <./concepts/playerhashes>`__
-  `States of the engine <./concepts/states>`__
-  `Variable Groups <./concepts/vargroups>`__
-  `mp\_map\_syncIn and mp\_map\_syncOut <./concepts/instancevars>`__
-  `VarGroup SyncTypes (mp\_type) <./concepts/synctypes>`__
-  `Tolerance <./concepts/tolerance>`__
-  `Buffer types <./concepts/buffer>`__
-  `CHAT Interface <./concepts/chat>`__
-  `**PLUS** - GMnet PUNCH <./concepts/udphp>`__
-  `**PLUS** - Master server (GMnet
   GATE.PUNCH) <./concepts/mediation>`__
-  `Signed packets <./concepts/signedpackets>`__
-  `The debug overlay <./concepts/debugoverlay>`__
-  `**PLUS** - GMnet GATE.TESTER <./concepts/htmt>`__

Basic Function Reference
~~~~~~~~~~~~~~~~~~~~~~~~

Sync Functions (mp\_*) * `mp\_sync <./functions/sync/mp_sync>`__
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  `mp\_unsync <./functions/sync/mp_unsync>`__
-  `mp\_stayAlive <./functions/sync/mp_stayAlive>`__
-  `mp\_add <./functions/sync/mp_add>`__
-  `mp\_addPosition <./functions/sync/mp_addPosition>`__
-  `mp\_addBuiltinBasic <./functions/sync/mp_addBuiltinBasic>`__
-  `mp\_addBuiltinPhysics <./functions/sync/mp_addBuiltinPhysics>`__
-  `mp\_setType <./functions/sync/mp_setType>`__
-  `mp\_tolerance <./functions/sync/mp_tolerance>`__
-  `mp\_map\_syncIn <./functions/sync/mp_map_syncIn>`__
-  `mp\_map\_syncOut <./functions/sync/mp_map_SyncOut>`__

Tools
^^^^^

-  `htme\_isLocal <./functions/tools/htme_isLocal>`__
-  `htme\_clientIsConnected <./functions/tools/htme_clientIsConnected>`__
-  `htme\_clientConnectionFailed <./functions/tools/htme_clientConnectionFailed>`__
-  `htme\_isStarted <./functions/tools/htme_isStarted>`__
-  `htme\_isServer <./functions/tools/htme_isServer>`__
-  `htme\_getPlayers <./functions/tools/htme_getPlayers>`__
-  `htme\_findPlayerInstance <./functions/tools/htme_findPlayerInstance>`__
-  `htme\_getPlayerNumber <./functions/tools/htme_getPlayerNumber>`__
-  `htme\_clientDisconnect <./functions/tools/htme_clientDisconnect>`__
-  `htme\_serverDisconnect <./functions/tools/htme_serverDisconnect>`__
-  `htme\_serverShutdown <./functions/tools/htme_serverShutdown>`__

CHAT Interface
^^^^^^^^^^^^^^

-  `mp\_syncAsChatHandler <./functions/chat/mp_syncAsChatHandler>`__
-  `mp\_chatGetQueue <./functions/chat/mp_chatGetQueue>`__
-  `mp\_chatSend <./functions/chat/mp_chatSend>`__
-  `htme\_chatGetMessage <./functions/chat/htme_chatGetMessage>`__
-  `htme\_chatGetSender <./functions/chat/htme_chatGetSender>`__

Online Lobby
^^^^^^^^^^^^

-  `udphp\_downloadServerList <./functions/lobby/udphp_downloadServerList>`__

LAN Lobby
^^^^^^^^^

-  `htme\_startLANsearch <./functions/lanlobby/htme_startLANsearch>`__
-  htme\_stopLANsearch

Global Sync
^^^^^^^^^^^

-  `htme\_globalGet <./functions/globalsync/htme_globalGet>`__
-  `htme\_globalSet <./functions/globalsync/htme_globalSet>`__
-  `htme\_globalSetFAST <./functions/globalsync/htme_globalSetFAST>`__

Event handlers
^^^^^^^^^^^^^^

-  `htme\_serverEventHandlerConnecting <./functions/events/htme_serverEventHandlerConnecting>`__
-  `htme\_serverEventHandlerDisconnecting <./functions/events/htme_serverEventHandlerDisconnecting>`__

Configuration
^^^^^^^^^^^^^

-  `htme\_init <./functions/config/htme_init>`__

More documentation may be added later. You can find a documentation of
every script in the header of the script files.

FAQ and More
~~~~~~~~~~~~

-  `Extending the Engine / Advanced Use <./more/extending>`__
-  `How to update <./more/update>`__

More will be added to this section later.

Support
~~~~~~~

**Please use the `forums <../../forum>`__ for support. We will answer
there.**
