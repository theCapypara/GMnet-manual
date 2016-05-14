Basic configuration
-------------------

In this tutorial we want to make a **simple platformer** with some neat
little extras to demonstrate what *GMnet ENGINE* can do. Our platformer
will have:

-  Walls/Players/Physics (obviously)
-  Multiple rooms
-  An overlay that shows connected players
-  A night and day cycle
-  A basic chat system

Adding the engine to a project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before we can get started, add the asset to an empty project.
Depending on what you want to do, you have three options.

-  If you want to **follow this tutorial yourself**, you should add
   **ALL scripts and sprites and the object** ``obj_htme`` to your
   project.
-  If you want to just **read through this tutorial** and test the
   demo game, **simply add everything**.
-  When starting completely blank or when you want to **add the engine to your own game**,
   add all folders named **htme** and **udphp** but not the *htme_demo*
   folders.

Configuration
~~~~~~~~~~~~~

Great! No matter what option you chose, you propably want to take a look
at the initiation and configuration, so let me walk you through.

Before we look at the configuration we check the initiation script.
**The init can be found in ``scripts/htme/htme_init``**.

The first thing you'll find under initiation is ``randomize();``.
That assures that the random operations Game Maker does are truly
random, which is important for the engine. This is good to know when you make your game.
Thats all for the initiation for now. Let's go to configuration.

**The configuration can be found in ``scripts/htme/htme_config``**.

First you see **debug level**. Valid options can be found
in the enum ``htme_debug`` and how debugging works is explained in the
comment. Leave it on the default option for now.

Let's skip ahead to **``self.global_timeout``**. That's actually the
only important configuration option and even that can stay on default if
you want. Timeout specifies after how many steps of inactivity the
connection between client and server will die and you will be
disconnected. The default is ``5*room_speed`` which basicly means 5
seconds. When client and server don't communicate to each other for 5
seconds, they are considered to be disconnected.

So yeah that was all there is to configure for now.

Follow the next steps of the configuration. They will explain how GMnet
ENGINE (or GMnet PUNCH to be precise) enables you to connect to other
players even behind a firewall.