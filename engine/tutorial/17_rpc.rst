Bonus: RPC
----------

`RPCs (Remote procedure
calls) <http://en.wikipedia.org/wiki/Remote_procedure_call>`__ are used
to execute scripts/code/functions remotely.

For the engine this means RPC enables you to execute scripts on other
clients / servers. After you finished this part of the tutorial you will
have a fully functional way of calling scripts via the network.

This tutorial will also show you how to send the value returned by the
RPC-called script back to the game of the player who called it.

**WARNING:** Please note that this tutorial does not cover any secruity
mechanisms. You propably want to restrict which scripts can be executed
and who and when clients can execute them and on which targets.

To make RPCs with GMnet ENGINE we will be using the `CHAT
Interface <concepts/chat>`__. Basic knowledge on how to use that is
required.

**This section is more advanced and good coding skills are required [
don't fear to try it out though :) ] **

Setup
~~~~~

First we need an object to listen for RPCs and to send RPCs through.

Create an object **obj\_htme\_rpc** with the events below, make it
**persistent** and make sure it is created when clients have connected
or a server was started, and get destroyed when the engine shuts down.

Create Event
^^^^^^^^^^^^

.. code-block:: gml

    mp_syncAsChatHandler("RPC");

Step Event
^^^^^^^^^^

.. code-block:: gml

    var queue = mp_chatGetQueue();
    while (ds_queue_size(queue) > 0) {
        htmerpc_recieve(ds_queue_dequeue(queue));
    }

**And create the two scripts ``htmerpc_recieve`` and ``htmerpc_send``.
The will be used to send and recieve RPC calls. And also create the
script ``htmerpc_callback``. This script will later be used to store the
values that the RPC-called scripts return.**

The RPC protocol
~~~~~~~~~~~~~~~~

We will now create a protocol to send and recieve the RPCs.

The message
^^^^^^^^^^^

Okay, so let's think about how we can "package" our RPCs.

Each RPC needs to contain a script name and it's argument. And each RPC
has one recipient that should execute the command.

Let's use a ds\_map for this. GameMaker allows you to convert ds\_maps
into `JSON <http://en.wikipedia.org/wiki/JSON>`__ which can be sent over
the network and then be decoded again.

Our message will be a ds\_map, turned into a json string with the
following contents:

::

        ds_map =>
           [id] => string
           [script] => string
           [argument_count] => real
           [argument0] => string or real (optional)
           [argument1] => string or real (optional)
           ...
           [argument12*] => string or real (optional)

``id`` is used to identify the RPC calls. You will see why this is
important later.

When we later convert these ds\_maps into JSON, the message will look
like this:

.. code-block:: json

    {"id":"foo","script":"scr_myscript","argument_count":2,"argument0":12.3,"argument1":"Hello World"}

\* Only 13 arguments can be used as the script ``htmerpc_send`` we will
create now can only take in 16 arguments, and two of them are used for
other things

Creating a script to send messages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| We are now going to write ``htmerpc_send``. This script should be used
  anywhere to send RPC commands.
| This script will need: \* The id of this RPC call. This is used to get
  the value that the script that was executed using this call later. \*
  The script to execute \* A target player (where the script should be
  executed) \* The arguments

So let's fill the script with this:

.. code-block:: gml

    ///htmerpc_send(id,script,to,[argument0...13])
    /* Sends RPC calls to another player */

    /* 
     * Turn script into a string. You call this function with (htmerpc(my_script,...); 
     * my_script will be turned into a number by Game Maker that identifies this script, 
     * we turn this into a string to send it over the network, because if you use 
     * different versions of your game, this id might not be the same for the same script.
     */
    var rid = argument[0]; 
    var script = script_get_name(argument[1]); 
    var to = argument[2]; //Hash of the player to send this to
    var rpc_argument;
    if (argument_count > 3) rpc_argument[0] = argument[3];
    if (argument_count > 4) rpc_argument[1] = argument[4];
    if (argument_count > 5) rpc_argument[2] = argument[5];
    if (argument_count > 6) rpc_argument[3] = argument[6];
    if (argument_count > 7) rpc_argument[4] = argument[7];
    if (argument_count > 8) rpc_argument[5] = argument[8];
    if (argument_count > 9) rpc_argument[6] = argument[9];
    if (argument_count > 10) rpc_argument[7] = argument[10];
    if (argument_count > 11) rpc_argument[8] = argument[11];
    if (argument_count > 12) rpc_argument[9] = argument[12];
    if (argument_count > 13) rpc_argument[10] = argument[13];
    if (argument_count > 14) rpc_argument[11] = argument[14];
    if (argument_count > 15) rpc_argument[12] = argument[15];

This "simply" processes the arguments for the script. All arguments for
the RPC script get written in the rpc\_argument array. You can also do
this using a loop by the way, which is far more elegant. We will use
argument\_count later again to see how many RPC arguments we have.

We actually don't have that much to do now. We create the ds\_map...

.. code-block:: gml

    var rpc_command = ds_map_create();

...fill it...

.. code-block:: gml

    rpc_command[? "id"] = rid;
    rpc_command[? "script"] = script;

    //If argument_count is 4, we have 4 arguments, which means 1 rpc argument etc.
    var rpc_argument_count = argument_count-3; 
    rpc_command[? "argument_count"] = rpc_argument_count;

    //Now we loop through all arguments and add them to the list:
    for (var i = 0; i < rpc_argument_count; i++) {
        rpc_command[? "argument"+string(i)] = rpc_argument[i];
    }

...and convert it to json:

.. code-block:: gml

    var message = json_encode(rpc_command);
    //After that we don't need the map anymore
    ds_map_destroy(rpc_command);

That's all. We can now send the message.
`mp\_chatSend <functions/chat/mp_chatSend>`__ allows a second argument
called ``to``. This is the hash of the player that should recieve the
message. Exactly what we need! We use a with-Block to call the
``mp_chatSend`` with our RPC object

.. code-block:: gml

    with (obj_htme_rpc) {
        mp_chatSend(message,to);
    }

The message is sent! Let's process it!

Recieving RPCs
~~~~~~~~~~~~~~

What's the point of sending RPCs if we can't recieve them, right?

In the step event we created earlier we already added a call to
``htmerpc_recieve`` with a message as argument. Let's create the script.

.. code-block:: gml

    ///htmerpc_recieve(message)
    /* Processes RPC calls*/
    var message = htme_chatGetMessage(argument0);
    var from = htme_chatGetSender(argument0);

Using `htme\_chatGetMessage <functions/chat/htme_chatGetMessage>`__ we
take the raw message and decode it to get the actual message. We also
store the hash of the player that sent the RPC, because at the end of
this script we want to send a RPC back containing the returned value of
the script. But we'll come to that in a bit.

Let's decode the ds\_map:

.. code-block:: gml

    var rpc_command = json_decode(message);

``rpc_command`` will now contain the ds\_map we created earlier. Magic!

Let us waste no time and execute the command. This can be done by
combining ``asset_get_index`` and ``script_execute``.
``asset_get_index`` turns the string that contains the script name back
into an id and ``script_execute`` executes the command using this id.

Because we also want to process the arguments, this may look a bit
ridiculous now, but it works:

.. code-block:: gml


    var rid = rpc_command[? "id"];
    var rpc_argument_count = rpc_command[? "argument_count"];
    var result;

    if (rpc_argument_count == 0) {
        result = script_execute(asset_get_index(rpc_command[? "script"]));
    }

    if (rpc_argument_count == 1) {
        result = script_execute(asset_get_index(rpc_command[? "script"]),rpc_command[? "argument0"]);
    }

    if (rpc_argument_count == 2) {
        result = script_execute(asset_get_index(rpc_command[? "script"]),rpc_command[? "argument0"],rpc_command[? "argument1"]);
    }

    /** CONTINUE THIS UNTIL 14 **/

    if (rpc_argument_count == 13) {
        result = script_execute(asset_get_index(rpc_command[? "script"]),rpc_command[? "argument0"],rpc_command[? "argument1"],rpc_command[? "argument2"],rpc_command[? "argument3"],rpc_command[? "argument4"],rpc_command[? "argument5"],rpc_command[? "argument6"],rpc_command[? "argument7"],rpc_command[? "argument8"],rpc_command[? "argument9"],rpc_command[? "argument10"],rpc_command[? "argument11"],rpc_command[? "argument12"]);
    }

And well... that's it. But wait - now we need to send the value that
this function returned back.

Returning the value and sending it back
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Everything we did so far was fine, but now what if we want to know what
the script returned?

Remember the script ``htmerpc_callback`` we created earlier? When we are
done executing the RPC script we send the returned value we stored in
``result`` above back to the sender of the RPC. This script will then
tell the author of the original RPC the returned value.

That means:

1. Player A sends RPC to Player B to run scr\_myscript which returns
   "Hi!".
2. Player B recieves the RPC, runs the script and stores the value in
   ``result``.
3. Player B sends RPC to Player A to run ``htmerpc_callback`` with the
   arguments being the ``id`` of the original call and the ``result``.
4. Player A recieves the RPC, runs the script, notices that it calls
   ``htmerpc_callback`` and therefor stops (otherwise this would be an
   endless loop).

Step 2 and 4 in script (add to the end of ``htmerpc_recieve``):

.. code-block:: gml

    //Only send returned value if this RPC isn't already about a returned value (otherwise this would result in an endless loop)
    if (rpc_command[? "script"] != "htmerpc_callback") {
        //Send returned value back via RPC
        //The id is not relevant for this because we don't track this RPC - we leave it empty.
        htmerpc_send("",htmerpc_callback,from,rid,result);
    }

    //Destroy the map, we don't need it
    ds_map_destroy(rpc_command);

The recieve-Script is now done. We now need to create
``htmerpc_callback`` and add a way to actually get the values.

Storing and retrieving the returned values
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

But before we do that, we need somewhere to store those values. Let's
use our ``obj_htme_rpc`` for that and a ds\_map. It will have the ids as
keys and the returned values as values.

Add it to the create event:

.. code-block:: gml

    self.returnedValues = ds_map_create();

Okay, so now let's create ``htmerpc_callback``, this script is actually
incredibly simple:

.. code-block:: gml

    ///htmerpc_callback(id,returnedValue)
    /* Reciveves the returned value of RPCs via RPC */

    ds_map_add(obj_htme_rpc.returnedValues,argument0,argument1);

That is all. Whenever a RPC call is sent, it will now add the returned
value to the map. You can get it anywhere by using code like this:

.. code-block:: gml

    ///Create event of some object - You can use htme_hash() to generate random ids
    self.rpc_id = htme_hash();
    htmerpc_send(self.rpc_id,my_cool_script,some_player_hash,0,"Test",3+2);

///Step event

.. code-block:: gml

    var returnedValue = ds_map_find_value(obj_htme_rpc.returnedValues,self.rpc_id);

    //ds_map_find_value returns undefined if the key was not found -> if the returnedValue has not been recieved
    //Please make sure the function actually returns something and returns something other than undefined, otherwise this code will never run.
    if (!is_undefined(returnedValue)) {

        show_message(returnedValue);
        //After that make sure to delete the key if you don't need it anymore
        ds_map_delete(obj_htme_rpc.returnedValues,self.rpc_id);

    }

| That's all!
| Here's a basic RPC protocol for you to improve on. Have any ideas? Be
  sue to leave them in our new forums!

**When using this for your game, be sure to include error handlers and a
secuity mechanism as explained at the top of the page.**
