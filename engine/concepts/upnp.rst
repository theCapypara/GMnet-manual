UPnP
----

UPnP stands for Universal Plug and Play.

GMnet ENGINE use UDP hole punching to make the NAT/router allow online connections.

UPnP automates the port forwarding on the users router or NAT. It sends a command to the router to forward a port.

But not all NATs allow UDP punch. The user must then manually port forward the server port (ex 6510)
or use other methods such as UDP Hole-Punching (as done by GMnet PUNCH) that can also allow online play without UPnP or port forwarding.

By enabling UPnP you allow users who don't forward their port and that are in
networks that don't support UDP Hole-Punching to play anyway.

When your users start the server, UPnP will try to port forward the server port for them.
You can enable UPnP in ``htme_config``.

.. note:: UPnP won't work 100% for everybody (even if UPnP is supported) when used with the GMNet PUNCH master server until version 1.4.0!

          But there is no harm in turning it on anyway.