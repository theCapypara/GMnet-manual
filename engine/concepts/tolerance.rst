Tolerance
---------

Using `mp\_tolerance <functions/sync/mp_tolerance>`__ you can give each
variable that is a real (a number) a tolerance range in that it will not
be chanegd locally. This is mainly used to make smooth movement and
prevent players from jumping arround a few pixels.

Take as an example the x position:

If the actual x-Position of an instance should be 12 but it's 15
locally, the change will not be applied locally if the tolerance is
greater than or equal 3.
