UPnP
----

UPnP stands for Universal Plug and Play. 
Punsh use UDP hole punching to make the nat/router allow online connections.
But not all nats allow UDP punsh. You must then manually port forward the server port (ex 6510). 
You can do this by enter the nats setup page. Open your browser and type in http://192.168.1.1/.
This may (if the ip is right) open the nats setup page where you can port forward the server port and allow online play.

But this can be automated by UPnP.
When you start the server UPnP will try to port forward the server port for you.
You can enable UPnP in ``udphp_config``.
