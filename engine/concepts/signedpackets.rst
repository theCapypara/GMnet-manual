Signed packets
--------------

Signed packets are a special type of packets that are guaranteed to
arrive.

Normally when using UDP multiplayer, packets are sent very fast on the
cost of reliability.

Signed packets give GMnet ENGINE the option to have packets that are
sent with the reliability of TCP. These are used with the sync types
SMART and IMPORTANT and some other internal operations.

You can also use them. Either by using the SMART and IMPORTANT sync
types or by using them with your own packets. For how see "`Extending
the Engine / Advanced Use <more/extending>`__".
