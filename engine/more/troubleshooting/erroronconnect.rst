Error on connect
----------------

Sometimes you may experience errors when you try connect. Here are some error messages and the solutions.

Port is a real
~~~~~~~~~~~~~~

.. code-block:: gml

    ERROR in
    action number 1
    of Step Event0
    for object obj_htme:

    Illegal argument type
    at gml_Script_htme_clientConnect (line 29) - network_send_udp( self.socketOrServer, self.server_ip, self.server_port, self.buffer, buffer_tell(self.buffer) );
    ############################################################################################
    --------------------------------------------------------------------------------------------
    stack frame is
    gml_Script_htme_clientConnect (line 29)
    called from - gml_Script_htme_step (line 59) - htme_clientConnect();
    called from - gml_Object_obj_htme_StepNormalEvent_1 (line 2) - htme_step();

Make sure you provide a real and not a string as port argument in ``htme_clientStart``.

.. code-block:: gml

    htme_clientStart(ip,real(port))
