Why do i control two instances
------------------------------

When you start two instances of your game you may experience that you control P1 and P2.
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