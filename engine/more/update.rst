How to update
-------------

When updating, check the changelog and this page to see which files have
changed. When you made changes to these files, make a backup and update
the asset.

After you are done updating, check what has changed (you might find
detailed information in the changelog) and merge the new version with
your changes.

Recent updates
~~~~~~~~~~~~~~

1.2.2 - CHAT Interface, Event Handlers, RPCs, MIT License
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  LICENSE CHANGED TO MIT
   Due to confusion about the GPLv3 license, I decided to change the
   license to the MIT license. This is way easier to understand for
   everybody. BY UPDATING YOU AGREE TO THIS NEW LICENSE. THIS LICENSE
   REPLACES THE OLD ONE.
-  Support for custom Event Handler for Connection/Disconnection on
   Server
   Also adds an easy way to reject players when they conect
-  Fixed a bug that prevented the game to be run with the YYC (thanks to
   Imtnt @gmc)
-  Server Shutdown Function added and automatic shutdown/disconnect if
   the htme object is destroyed / game is ended
-  PLUS/UDPHP : UDPHP 1.2.1 - Fixed an issue where servers and client
   could not connect to each other when the master server was not
   reachable.
-  Added CHAT Interface:
   This is a new set of functions that allow you to send and recieve
   string messages in a more clasic way. The manual was updated so the
   Chat Tutorial now uses this new way of syncing (an RPC tutorial was
   also added to the manual; see below).
-  Updated debug overlay to include debug information about the CHAT
   Interface
-  Fixed a bug, where in rare cases clients could start syncing before
   they got their player hash which lead to invalid instances being
   synced and mayor desync
-  MANUAL (http://htme.parakoopa.de/manual) :
-  Added manual pages for the event handler scripts
-  Added Tutorial Chapter Bonus 4 - Event Handlers for
   Connecting/Disconnecting
-  Added manual page for htme\_shutdown
-  Added manual page for htme\_globalSyncFAST
-  Added manual page for the CHAT Interface and all it's functions
-  Rewrote Tutorial 11 - Chat (it is now using the CHAT Interface)
-  Added Tutorial Chapter Bonus 5 - RPC
-  Updated debug overlay manual
-  Master Server is now on Version 1.2.3, you might want to update, some
   critical bugfixes were made.
-  **We now have a forum: http://htme.parakoopa.de/forum - Check it out
   - This is now the main place for support! **

1.2.1 - Introducing a better online lobby and a LAN lobby for all!
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This update improves the ONLINE lobby by adding fltering and sorting
mechanisms. Check out the `updated tutorial <tutorial/13_lobby>`__! Also
we added a seperate `lobby for LAN Servers <tutorial/15_lanlobby>`__,
the master server was HUGELY updated and we are happy to introduce a
`testing tool for master servers <concepts/htmt>`__

-  Added a `LAN lobby <tutorial/15_lanlobby>`__.
-  UDPHP/PLUS: Added a new lobby system that supports filtering
-  UDPHP/PLUS: Added support for new registration and sending version
   number
-  UDPHP/PLUS: Changed it so the server only reconnects to the master
   server if it lost connection
-  **You need to update the master/mediation server if you are a GMnet
   ENGINE!!**

Master server changelog
'''''''''''''''''''''''

Master server Version 1.2.0

-  Added the possibility to name the server
-  Added --version parameter
-  Added --testing paramter to be tested via HTMT.
-  Added multiple testing commands
-  Added a filter for a minimum required udphp version
-  Changed registration so it requires the udphp version of the server
   that wants to register
-  Fixed bugs in server destruction
-  Added a createdTime field to the servers
-  Added filter and sorting methods to the lobby

**CHANGED FILES IN 1.2.1:**

::

        scripts/htme_init.gml
        objects/obj_udphphtme_lobby.object.gmx
        scripts/udphp_config.gml
        scripts/udphp_downloadServerList.gml
        scripts/udphp_serverCommitData.gml
        scripts/udphp_Punch.gml
        scripts/htme_getDataServer.gml
        scripts/htme_getLANServers.gml
        rooms/htme_lanlobby.room.gmx
        scripts/htme_networking_searchForBroadcasts.gml
        objects/htme_obj_lanlobbydemo.object.gmx
        objects/htme_obj_menu.object.gmx
        scripts/htme_serverBroadcast.gml
        scripts/htme_serverStart.gml
        scripts/htme_startLANsearch.gml
        scripts/htme_stopLANsearch.gml
        scripts/htme_step.gml

1.2.0 - Debug overlay and graceful discon
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**I recommend to reinstall GMnet ENGINE, meaning removing the old asset
and adding the new one. Make sure to backup your config.**

-  Added htme\_serverDisconnect and htme\_clientDisconnect to gracefully
   kick players or disconnect from the server.
-  Added a debug overlay. All information about that
   `here <concepts/debugoverlay>`__.
-  Changed visuals of demo project
-  UDPHP (PLUS only): Fixed bug that resulted in not closing old TCP
   connections on the servr when reconnecting.
-  Added globalSetFAST. Same as globalSet but with the fast sync type.

**CHANGED FILES IN 1.2.0:**

::

        objects/htme_obj_playerlist.object.gmx
        objects/obj_htme.object.gmx
        rooms/htme_rom_demo.room.gmx
        rooms/htme_rom_demo2.room.gmx
        scripts/htme_clientDisconnect.gml
        scripts/htme_clientNetworking.gml
        scripts/htme_clientShutdown.gml
        scripts/htme_debugOverlayEnabled.gml
        scripts/htme_debugoverlay.gml
        scripts/htme_doDrawInstanceTable.gml
        scripts/htme_doGlobalSync.gml
        scripts/htme_doInstAll.gml
        scripts/htme_doInstCached.gml
        scripts/htme_doInstInvisible.gml
        scripts/htme_doInstVisible.gml
        scripts/htme_doMain.gml
        scripts/htme_doMain_new.gml
        scripts/htme_doOff.gml
        scripts/htme_doPlayers.gml
        scripts/htme_doSignedPackets.gml
        scripts/htme_doStateInstAll.gml
        scripts/htme_doStateInstCached.gml
        scripts/htme_doStateInstInvisible.gml
        scripts/htme_doStateInstVisible.gml
        scripts/htme_doStateMain.gml
        scripts/htme_doStateOff.gml
        scripts/htme_do_createMicro.gml
        scripts/htme_dotbd.gml
        scripts/htme_findPlayerInstance.gml
        scripts/htme_globalSetFast.gml
        scripts/htme_globalSet_new.gml
        scripts/htme_init.gml
        scripts/htme_sendGSFast.gml
        scripts/htme_sendGS_new.gml
        scripts/htme_serverDisconnect.gml
        scripts/htme_serverKickClient.gml
        scripts/htme_serverNetworking.gml
        scripts/htme_serverProcessKicks.gml
        scripts/htme_serverStart.gml
        scripts/htme_step.gml
        scripts/mp_add.gml
        scripts/udphp_serverPunch.gml
        sprites/htme_spr_door.sprite.gmx
        sprites/htme_spr_player.sprite.gmx
        sprites/images/htme_spr_door_0.png
        sprites/images/htme_spr_player_0.png
        sprites/images/htme_spr_wall_0.png

1.1.0 - Introducing: Global Sync
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Added Global Sync to sync global variables that are read- and
   writeable at any time by all clients and the server.

**CHANGED FILES IN 1.1.0:**

::

    htme_clientNetworking.gml
    htme_clientStart.gml
    htme_init.gml
    htme_serverEventPlayerConnected.gml
    htme_serverNetworking.gml
    htme_serverStart.gml
    htme_recieveGS.gml (added)
    htme_sendGS.gml (added)
    htme_globalGet.gml (added)
    htme_globalSet.gml (added)

1.0.0 - The lobby update
^^^^^^^^^^^^^^^^^^^^^^^^

`**Please see this page for more information** <lobbyupdate>`__

0.6.0 - The performance update
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**The great performance update!** - ADDED A NEW LICENSE. BY UPDATING YOU
AGREE TO THIS NEW LICENSE. -- The license is still GPLv3, but it comes
with an additional permission to create games in Game Maker without
having you to provide the source code of your game when using the
Mutliplayer Engine - Made isLocal faster - Improved behaviour and
performance of signed packets. Reliable data will no longer by sent if
new data is available - Replaced most of the maps with lists, resulting
in a huge performance boost! - Fixed crashes and desyncs on certain
events - Fixed a mayor memory leak and improved memory managment - COMES
WITH udpph 1.1.2. - No mayor changes to the local manual! - Online
manual was updated with changelog.

**CHANGED FILES IN 0.6.0:**

::

    htme_cleanUpInstance.gml
    htme_clientBroadcastUnsync.gml
    htme_clientStart.gml
    htme_createSignedPacket.gml
    htme_createSingleSignedPacket.gml
    htme_forceSyncLocalInstances.gml
    htme_init.gml
    htme_isLocal.gml
    htme_recieveSignedPackets.gml
    htme_recieveVarGroup.gml
    htme_removeSignedPacket.gml
    htme_removeSignedPacketsByCatFilter.gml
    htme_roomstart.gml
    htme_sendSignedPacket.gml
    htme_sendSignedPackets.gml
    htme_serverBroadcastUnsync.gml
    htme_serverCreateSPForAllCheckRoom.gml
    htme_serverEventPlayerConnected.gml
    htme_serverEventPlayerDisconnected.gml
    htme_serverKickClient.gml
    htme_serverNetworking.gml
    htme_serverRecreateInstancesLocal.gml
    htme_serverRemoveBackup.gml
    htme_serverSendAllInstances.gml
    htme_serverStart.gml
    htme_serverSyncPlayersUDPHP.gml
    htme_syncInstances.gml
    htme_syncSingleVarGroup.gml
    mp_add.gml
    mp_unsync.gml
    udphp_stopServer.gml 

**udphp CHANGELOG:**

udphp 1.1.2: \* Fixed stopServer not working anymore

udphp 1.1.1: \* Fixed some bugs that were created with the changes in
1.1.0. ...

0.5.0
^^^^^

Initial release
