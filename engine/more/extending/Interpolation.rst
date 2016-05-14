Interpolation
-------------

You will notice that sending keystrokes are not always optimal.
Your player object will do some jittering when move. And you teleport from place to place sometimes.
Here is a video to show why you need interpolation:

.. raw:: html

   <iframe width="420" height="315" src="https://www.youtube.com/embed/3nsq3s9jxys" frameborder="0" allowfullscreen>

.. raw:: html

   </iframe>

In short interpolation means that you travel from point 1 to point 2. But not by using keystrokes. 
Instead we use positions and interpolate (travel smootly) from point 1 to point 2. But it can be any 2 points.
It can be one x position to another x position. It can be one image_angle to another image_angle. You can interpolate
any values to make a smooth look.

To code this we use the demo project as template. In this example we only interpolate the x and y position. 
Start in the htme_obj_player create event:

.. code-block:: gml

    mp_addPosition("Pos",600*room_speed);

We only need to update the position once we enter the room. The interpolation will fix the rest.
We are still in the create event and add this code after the ``mp_sync()``:

.. code-block:: gml

    self.xpos=x;
    self.ypos=y;
    stepsToWaitUntilSendNextPos=6;
    mp_add("interpolation","xpos,ypos",buffer_s16,stepsToWaitUntilSendNextPos);

This will sync the position to the other clients. We also need some variables to hold some values:

.. code-block:: gml

    /// Interpolation setup
    // use when check if new pos received
    last_received_xpos=-1;
    last_received_ypos=-1;
    // interpolate values each step
    travel_every_step_x=-1;
    travel_every_step_y=-1;
    // steps we interpolate
    travel_every_step_counter=-1;
    // save new pos if the other interpolation is not done yet
    new_queue=ds_queue_create();

These will keep track of the last received position. So we know if we moved. 
And in interpolation we move some in each step so we use varialbes to hold the travel speed in.
We also want to stack the positions if receive a new position before we are done.

Now brace yourself and add this in the Step begin event:

.. code-block:: gml

    if (htme_isLocal()) {
        // ====================
        // Run on THIS computer (LOCAL)
        // ====================
        // This script here only run if the instance is local (our player on this computer)
        // The engine will create our player on the other players screens
        // So we now got our own player on this computer and the other players computers
        // We must control what we want to send to our player on the other players computer
        // Here you should add controls over your player
        // if we got this inside if (htme_isLocal()) {
        // This will only run on your computer and not on the other players computers
        // We add some info to send to our player on the other computers
        self.xpos=x;
        self.ypos=y;
        // We will set this on every step but the engine will only send it every
        // mp_add("interpolation","xpos,ypos",buffer_s16,stepsToWaitUntilSendNextPos);
        //                                                 ^
        //                                                 6
        // Every 6 steps we send this info to our player on the other computers
    } else {
        // ==============================
        // Run on OTHER players computers (NON LOCAL)
        // ==============================
        // This script here only run on the other players screens
        // Here you should add what will happen on other players screens
        // in the end step we use mp_map_syncOut() this is used to receive
        // information from mp_map_syncIn()
        // We now want to use the information we got from our player on our computer
        // on this player computer
        // So in the above we set 
        // self.xpos=x;
        // self.ypos=y;
        // The multiplayer engine sent it to this object on the other computer
        // The engine also create a new instance of this object. And now the engine
        // wait until you send information to it from your computer. Like you xpos and ypos
        // So what should happen on the other players screen with our xpos and ypos 
        // we got from your computer?
        // We want to interpolate.
        // This will run every step but we dont get new positions every step do we
        // So we must check when new information is received.
        if self.xpos!=last_received_xpos or self.ypos!=last_received_ypos {
            // We got a different xpos or ypos value from our computer
            // Let us save this new pos in a queue
            // We always save the new pos in a queue
            // Because we might get a new pos before we are done with the first one
            ds_queue_enqueue(new_queue,self.xpos,self.ypos);
            // In a queue the values get out as they came in so if we add
            // Its like puting cards one each other and draw them from below
            // What comes in first draw first
            // Ex you enqueue number 3,8,5,2,7,4 and then dequeue 4 of them
            // you get 3 first then 8,5 and 2
            // next time you dequeue you get 7 and 4
            // Now lets save this pos as the last
            last_received_xpos=self.xpos;
            last_received_ypos=self.ypos;
        }
    
        // Now we check the queue if we got a new pos in it
        if ds_queue_size(new_queue)>0 {
            // First we check if we allready interpolating
            // If we do then we must wait until it's done and then we can do the new pos
            if travel_every_step_counter<1 {
                show_debug_message("x:" + string(x) + " y:" + string(y))
                // We now want to smootly move our player object on this player computer
                // to that new x pos or y pos
                // get the new x and y pos from the queue
                // we saved x first and the y so
                var newx=ds_queue_dequeue(new_queue);
                // and then get y
                var newy=ds_queue_dequeue(new_queue);
                show_debug_message("new x:" + string(newx) + " new y:" + string(newy))
                // Ok now we must move it some pixels at a time every step
                // And we know how long it took to travel this new pos
                // We sent this new info every 6 step so from x to new x it took 3 steps
                            
                // Now we check if we got many new pos saved
                // If we got to many our player on the other computer will
                // fall back some and desync
                // So we check if we got 3 new pos then we can just skip one and travel
                // to the next
                if ds_queue_size(new_queue)>2 {
                    // We got to many new pos lets take one more out
                    var newx=ds_queue_dequeue(new_queue);
                    var newy=ds_queue_dequeue(new_queue);  
                    // But now we took 2 new values
                    // And we know it took 6 steps to travel to one new pos
                    // so if we take out 2 new pos it must have taken 12 steps 
                    // to travel there. But to avoid that we fall back again
                    // lets only do it in 11 steps
                    // We set the stepsToWaitUntilSendNextPos in the create event
                    var StepsWeTravel=(stepsToWaitUntilSendNextPos*2)-1;           
                } else {
                    // Set time it took to travel to this new pos
                    // We only took one new pos so it took 6 steps to travel there
                    var StepsWeTravel=stepsToWaitUntilSendNextPos; 
                }
                // First we check the distance from current pos on this computer (x,y)
                // To your new position we sent to this copmputer (xpos, ypos)
                var distance_to_move_x=newx-x;
                var distance_to_move_y=newy-y;
                // Then we calc how much we must move to reach the new pos in the steps we want
                travel_every_step_x=distance_to_move_x/StepsWeTravel;
                travel_every_step_y=distance_to_move_y/StepsWeTravel;
                // We want to only move our player on other computer in 6 steps (or more if we took 2 new pos) so lets count it
                travel_every_step_counter=StepsWeTravel;
            }
        }
        // We now must handle the movement
        // First we check if we got any counts left
        if travel_every_step_counter>0 {
            // Ok we must travel some
            // Let add it to x and y on this computer
            // Remember this script will never run on your computer where you control the player
            // Only on the other players computers
            show_debug_message("travel x:" + string(travel_every_step_x) + " travel y:" + string(travel_every_step_y));
            x+=travel_every_step_x;
            y+=travel_every_step_y;
            show_debug_message("new x:" + string(x) + " new y:" + string(y));
            // Now we remove one count
            travel_every_step_counter-=1; // same as travel_every_step_counter=travel_every_step_counter-1;
            show_debug_message("steps left:" + string(travel_every_step_counter))
            // When it reach 0 we will check if we got a new pos we can interpolate to
        }
    }

    // COMMON
    // This will run on this computer and the other computers
    // The mp_map_syncIn only run on the local. If we are on the remote it will just ignore this
    mp_map_syncIn("xpos",self.xpos);
    mp_map_syncIn("ypos",self.ypos);

I hope you got all.

The last one is in the step end event:

.. code-block:: gml

    self.xpos = mp_map_syncOut("xpos", self.xpos);
    self.ypos = mp_map_syncOut("ypos", self.ypos);

This will now interpolate the position and make your player move smootly from one position to the next.
You can also download a demo here:
https://drive.google.com/file/d/0BxE4k4xEiNO2azAzNkZObUV0NnM/view?usp=sharing