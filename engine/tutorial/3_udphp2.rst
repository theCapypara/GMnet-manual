Hosting a master server
-----------------------

.. note:: This topic requires GMnet PUNCH enabled.

.. note:: GMnet GATE PUNCH is outdated and will be replaced by a new master server in the next version.

To use the magic of *GMnet PUNCH* you need to host a
mediation/master/rendevouz server. The server is a small application
written in Java that needs to be run on a server **with a forwarded/open port**.

To explain why you need this, let me explain how the hole punching
works:

-  The server connects with the master server (GMnet GATE.PUNCH)
   and its port and ip get registered.
-  When the clients want to connect
   to this server, his port and ip also get registered and sent to the
   server. And the client gets the ip and port of the server.
-  Now both send UDP packets to each other at the same time: The hole is punched.

We need the master server (GMnet GATE.PUNCH) because we need to make the
server aware of the fact that a client wants to connect.

The download can be found here:

http://gmnet.parakoopa.de/gatepunch

The server is very basic, feel free to adjust it to your needs.

Currently the server binary listens on **port 6510** and there to change
it if you don't want to compile the server yourself, but we will add
that option in the future.

To start it, run: ``java -jar gmnet_gate_punch.jar`` from the folder you
saved the server in. Under Windows you might need to replace ``java``
with the full installation path of java. Under linux I recommend
``screen`` to run it in the background on a server.

Hosting
~~~~~~~

For cheap hosting I personally recommend **digitalocean**. Server start
at 0.0015 per hour (5 per month) and you can cancel at every
time.

Google yourself a promo code and you might get two months for free.
There are also tutorial on how to set up java on these servers. They are
basically linux servers with complete access.

If you want to use digitalocean, please use this code to register:
https://www.digitalocean.com/?refcode=1bff6d6dff1a

Some tutorials
^^^^^^^^^^^^^^

If you want to know how to login to the server:
`How To Create Your First DigitalOcean Droplet Virtual Server`_

For some basic commands and stuff:
`An Introduction to Linux Basics`_

If you want to install java:
`How To Install Java on Ubuntu with Apt-Get`_

For transfering the master server:
`How To Use Filezilla to Transfer and Manage Files Securely on your VPS`_

[You can skip the stuff with the keyfile and everything. Simply install
filezilla and connect to sftp://yourip with your username and password]

When you are done simply execute ``java -jar gmnet_gate_punch.jar``

As I said, I recommend install screen, it allows you to run commands
even if you are not logged in, running in the background and you can
just switch to them at any time:
`How to Install and Use Screen on an Ubuntu Cloud Server`_

You can also create an autostart service for the server and run it on startup.

.. _How To Create Your First DigitalOcean Droplet Virtual Server: https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server
.. _An Introduction to Linux Basics: https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-basics
.. _How To Install Java on Ubuntu with Apt-Get: https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get
.. _How To Use Filezilla to Transfer and Manage Files Securely on your VPS: https://www.digitalocean.com/community/tutorials/how-to-use-filezilla-to-transfer-and-manage-files-securely-on-your-vps
.. _How to Install and Use Screen on an Ubuntu Cloud Server: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-screen-on-an-ubuntu-cloud-server