Setting up the basic platformer
-------------------------------

We now need to create a simple platformer. Since **this is not supposed
to be a tutorial on platformers**, and the platformer we are going to
use is simple and pretty bad, simply follow the instructions and copy
the code.

1. Setup our game room
~~~~~~~~~~~~~~~~~~~~~~

Give the game room ``htme_rom_demo`` we created a nice **background
color** and the dimensions **800x600**. For this demo, we are not going
to use views.

2. Create a wall
~~~~~~~~~~~~~~~~

Create a solid object, called ``htme_obj_wall``. Give it the sprite
``htme_spr_wall``. This is our new wall. Place it into the game room,
build some walls, a floor and maybe some platforms.

3. Create the player object
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Next we are going to create our player.

Create the object ``htme_obj_player`` and give it the sprite
``htme_spr_player``.

Into the **create-Event** put the following code:

.. code-block:: gml

    ///Setup basic stuff for the demo platformer.
    self.pressed_jump = false;
    self.pressed_left = false;
    self.pressed_right = false;
    self.name = "";

    /** Totro generates random names and is not part of the main engine, it's
      * another marketplace asset by me :)
      */
    var ttr = totro(5,7,1);
    self.name = ttr[0];
    /** Gives this player a random color. */
    self.image_blend = irandom(16777215);
    }

The ``self.pressed...`` variables will store if our player pressed the
buttons to move or to jump. We need to store this in a variable as a
preperation for later, when we want to add the player to the engine. But
you'll see :).

Into the **step event** put the following code:

.. code-block:: gml

    ///Perform platforming!
    //This is a very basic example of a platformer. You should not program your physics like this!

    if (place_free(x, y+1)) {
       gravity = 0.2;
    } else {
       gravity = 0;
       vspeed = 0;
    }

    self.pressed_jump = keyboard_check(vk_space);
    self.pressed_left = keyboard_check(vk_left);
    self.pressed_right = keyboard_check(vk_right);

    if (self.pressed_jump && (!vspeed)) {
        vspeed = -12
        image_xscale = 1;
        image_angle = 90;
    }
    if (self.pressed_right) {
        x+=10;
        image_xscale = 1;
        image_angle = 0;
    }
    if (self.pressed_left) {
        x-=10;
        image_xscale = -1;
        image_angle = 0;
    }
    if (vspeed < 0) vspeed=vspeed+gravity;

As you can see, we currently just put the button presses into the
variables ``self.pressed...`` and check them. We will change that later.

Now create a **Collision with htme\_obj\_wall event** and put the
following code in it:

.. code-block:: gml

    ///Set speed to 0 when hitting a top wall
    if (!place_free(x, y-16)) {
        move_contact_solid(90,-1);
        vspeed = 0;
    }

    if (!place_free(x, y+16)) {
       move_contact_solid(270,-1);
       gravity = 0;
       vspeed = 0;
    }

Into the **draw event**, we will put some code to draw the name we
randomly generated in the create event. First put "**draw self**"" into
the event and then this code:

.. code-block:: gml

    ///Draw nameplate
    draw_set_color(image_blend);
    draw_set_halign(fa_center);
    draw_text(x,y-sprite_yoffset-5-string_height(self.name),self.name);
    draw_set_halign(fa_left);
    draw_set_color(c_white);

Basic platformer: Done!

4. Test
~~~~~~~

Start the game and then start the server. You can now test out how bad
the platformer really is. But hey, it does the job. The next tutorial is
actually related to the engine again.

.. figure:: images/1.PNG
   :alt: How it should look like

   How it should look like
