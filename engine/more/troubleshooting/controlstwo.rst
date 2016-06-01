Why do i control two instances
------------------------------

When you start two instances of your game you may experience that you control P1 and P2.
This may be because of missing htme_isLocal or windows may send the controls to both games at the same time.
Here are some thins you can try.

Use htme_isLocal()
~~~~~~~~~~~~~~~~~~

You must make sure that all your keyboard and mouse inputs are inside a ``htme_isLocal()`` statement like this:

.. code-block:: gml

    if (htme_isLocal()) {
        self.pressed_jump = keyboard_check(vk_space);
        self.pressed_left = keyboard_check(vk_left);
        self.pressed_right = keyboard_check(vk_right);
    }

This will make sure that only the local player run the control code.

Use Dual window extension
~~~~~~~~~~~~~~~~~~~~~~~~~

With this extension game maker will start 2 games when you test them in game maker.
When you click one window the other may not receive the controls.
Import this extension:
https://drive.google.com/file/d/0BxE4k4xEiNO2dEY5bUZ0dmo1b1E/view?usp=sharing
And add this object in the first room:
https://drive.google.com/file/d/0BxE4k4xEiNO2NW81Q1FnOTdsUUU/view?usp=sharing

Use Windows exe and game maker player export
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can also try export the game to windows exe and then run the game in game maker with game maker player export selected.
This may stop windows to send the input to both games at the same time.