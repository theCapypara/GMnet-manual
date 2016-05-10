Buffer types
------------

When using `mp\_add <functions/sync/mp_add>`__ you need to specify a
buffer type that specifys as which datatype the information is sent.
This is set for all variables in the `Variable
Groups <concepts/vargroups>`__.

The buffer types are the same as the ones `used by Game
Maker <http://docs.yoyogames.com/source/dadiospice/002_reference/buffers/buffer_write>`__.

Strings
~~~~~~~

``buffer_string``

Do not use ``buffer_text``. It's not supported.

Booleans (Reals with 0/1; false/true)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``buffer_bool``

Reals (Numbers)
~~~~~~~~~~~~~~~

From `the Game Maker
manual <http://docs.yoyogames.com/source/dadiospice/002_reference/buffers/buffer_write>`__:

+-------------+--------------+
| Type        | Desciption   |
+=============+==============+
| buffer\_u8  | An unsigned, |
|             | 8bit         |
|             | integer.     |
|             | This is a    |
|             | positive     |
|             | value from 0 |
|             | to 255.      |
+-------------+--------------+
| buffer\_s8  | A signed,    |
|             | 8bit         |
|             | integer.     |
|             | This can be  |
|             | a positive   |
|             | or negative  |
|             | value from   |
|             | -128 to 127  |
|             | (0 is        |
|             | classed as   |
|             | positive).   |
+-------------+--------------+
| buffer\_u16 | An unsigned, |
|             | 16bit        |
|             | integer.     |
|             | This is a    |
|             | positive     |
|             | value from 0 |
|             | - 65,535.    |
+-------------+--------------+
| buffer\_s16 | A signed,    |
|             | 16bit        |
|             | integer.     |
|             | This can be  |
|             | a positive   |
|             | or negative  |
|             | value from   |
|             | -32,768 to   |
|             | 32,767 (0 is |
|             | classed as   |
|             | positive).   |
+-------------+--------------+
| buffer\_u32 | An unsigned, |
|             | 32bit        |
|             | integer.     |
|             | This is a    |
|             | positive     |
|             | value from 0 |
|             | to           |
|             | 4,294,967,29 |
|             | 5.           |
+-------------+--------------+
| buffer\_s32 | A signed,    |
|             | 32bit        |
|             | integer.     |
|             | This is a    |
|             | positive     |
|             | value from 0 |
|             | to 264 - 1.  |
+-------------+--------------+
| buffer\_u64 | An unsigned  |
|             | 64bit        |
|             | integer.     |
|             | This can be  |
|             | a positive   |
|             | or negative  |
|             | value from   |
|             | -(263) to    |
|             | 263 - 1.     |
+-------------+--------------+
| buffer\_f32 | A 32bit      |
|             | float. This  |
|             | can be a     |
|             | positive or  |
|             | negative     |
|             | value within |
|             | the same     |
|             | range as a   |
|             | 32 bit       |
|             | signed       |
|             | integer.     |
+-------------+--------------+
| buffer\_f64 | A 64bit      |
|             | float. This  |
|             | can be a     |
|             | positive or  |
|             | negative     |
|             | value from   |
|             | -(263) to    |
|             | 263 - 1.     |
+-------------+--------------+

Floats are numbers with commas (3,2), Integers are numbers without (3).
When syncing a number with commas as an Integer, the value will be
rounded.
