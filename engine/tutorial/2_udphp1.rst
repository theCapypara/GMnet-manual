Setup GMnet PUNCH
-----------------

.. note:: This topic requires GMnet PUNCH enabled. More information below.

If you want *GMnet ENGINE* can be used to connect players
**even if the do not forward ports in their firewall**.

To understand this, you need to know, that whenever you want to play a
game with someone there are three options:

-  Dedicated servers to play on, like most shooters have
-  Forwarding a port on the servers firewall, most common when playing
   strategy games or hosting an own dedicated server of some game
-  "Hole-Punching" - **GMnet PUNCH**, which ships with GMnet ENGINE version,
   allows UDP Hole Punching. This technique allows two players to connect
   to each other even when no ports are forwarded at all. This works most
   of the time, however not always. Especially in mobile networks or buisness
   networks that might fail. Hole Punching is often used by many games where
   multiplayer should be easy to do by the user.

That means if you *disable GMnet PUNCH*, your players either can't
play together online, only locally, or the server has to open ports.

GMnet PUNCH configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

In ``htme_init`` there are several variables you need to change to use
*GMnet PUNCH*.

``self.use_udphp``: This is the most obvious one. Set this to
**true**, to enable GMnet PUNCH.

``self.udphp_master_ip`` and ``self.udphp_master_port``: You
need to set these to the ip and the port of your mediation server. What
a mediation server is, is explained in the next section. You basically
need to host a server, to which server and clients connect to share
their information.

``self.udphp_rctintv``: How often (in steps) the server should
reconnect to the mediation server to make sure it is still connected. It
is important that the server is connected to the mediation server, so
don't set this too high. The default option should be fine.

If you don't have a server yet you can use the ip 95.85.63.183 and the
port 6510 for testing only.