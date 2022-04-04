# oase-wireshark
Wireshark LUA script for analysing Oase UDP traffic

For my home automation project I wanted to be able to send commands directly to Oase FM Master. To make this happen I wrote LUA script for Wireshark to analyze the communication.

The controller operates on UDP port 5959 and it came out to be quite simple...

Basicly all what I need is to turn on/off the outlets which could be done with following command

<pre>
5c 23 4f 41 0d 00 00 00 02 0b 00 c4 00 00 00 00 04 00 00 00 00 00 00 00 00 64 02 01 ff
xx xx xx xx .............................................................................. magic string
            ll hh ........................................................................ data length
                        ?? ............................................................... 
                           xx ............................................................ sequence number
                              xx ......................................................... direction (0x00 - to controller; 0xff - from controller)
                                 xx ...................................................... command code
                                    ?? ?? ?? ?? ..........................................
                                                xx xx xx xx xx xx xx xx xx xx xx xx xx ... command data (of hh*256+ll length)
                                                
                                                                                 xx ...... for 0xc4 command here is the outlet index (0 .. 4, where 4 is dimmer)
                                                                                    xx ... for 0xc4 command here is the instensity (for dimer) or on (0xff) / off (0x00) value to be set
</pre>

Enjoy ;)



