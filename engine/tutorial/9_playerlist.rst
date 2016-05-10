Overlay that shows the name of connected players
------------------------------------------------

We will now create a list that is displayed in the top left corner of
the screen and will look something like this:

.. figure:: images/3.PNG
   :alt: A preview of the player list

   A preview of the player list

**Create a new object** ``htme_obj_playerlist`` with no sprite, make it
persistent so it exists in both game rooms, and **place it** in
``htme_rom_demo``.

This new object is actually not going to be added to the engine. This
object will simply look for all existing ``htme_obj_player`` instances
and write their metadata on the screen.

| The only thing we'll need is a **Draw-Event**.
| Let's start with drawing the word "Players:" on screen:

.. code-block:: gml

    draw_set_color(c_white);
    draw_text(40,35,"Players:");

Okay, cool, cool. But how on earth do we get all player instances? There
are two possibilites:

1. You could use ``with htme_obj_player {/*Code*/}`` to loop through all
   player instances
2. The engine provides some tools to get a list of all connected players
   and a function to get an instance that is controlled by a particular
   player.

In our case the first solution is the easiest. However we want to teach
you what you can do with the engine, and so **we are going to use the
second method**. There might be cases where looping through all
instances of an object would be simply to much, for example if you have
a race game with 2 players and 6 cpus and you only want to get data of
the connected players.

.. code-block:: gml

    var playerlist = htme_getPlayers();

This will give you a ``ds_list`` containing the hashes of all players.
Each player is identifed by a random 8 character hash.

To loop over this list, add the following for-loop:

.. code-block:: gml

    for(var i = 0;i<ds_list_size(playerlist);i++) {
        var player = ds_list_find_value(playerlist,i);
    }

``player`` will now be the playerhash of a player. We use this hash to
get a player instance of this player. **Inside the for loop after
``var player =...`` insert the following:**

.. code-block:: gml

    var instance = htme_findPlayerInstance(htme_obj_player,player);

This will either **return an instance or -**\ 1. It will **return -1
when the player is in another room**, because no instance for this
player exists. **And that's a problem**.

Because that means we can't actually get the name of the player to
display it then. That's a limitation because we store the player name
with our player object. After this tutorial is over you should be able
to solve this issue, and I challenge you to do so!

Because of this limitation we will simply show "(other room)" in a grey
color, when the player instance does not exist:

.. code-block:: gml

    if (instance != -1) {
        var name = (instance).name;
        var _image_blend = (instance).image_blend;
    } else {
        var name = "(Other room)";
        var _image_blend = c_gray;
    }

**``name`` now contains the name of the current player and
``_image_blend`` the color.**

**The following code will draw the sprite and the name:**

.. code-block:: gml

    //Draw small player icon
    draw_sprite_ext(htme_spr_player,0,50,(i)*20+70,0.5,0.5,0,_image_blend,1);
    //Draw player name
    draw_set_colour(_image_blend);
    draw_text(70,(i)*20+62,name);

Remember, all of this must go into the for-loop.

Start the game and test it out, our player list should work just fine.