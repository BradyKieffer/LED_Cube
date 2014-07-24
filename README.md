LED_Cube
========

Brady Kieffer - 24-07-2014

NOTE:  I assume no responsibility for any damage to one's Arduino.
       Make sure you have the correct hardware.
       
I followed this tutorial for making the cube:
  http://www.instructables.com/id/4X4X4-LED-Cube-w-Arduino-Uno/?ALLSTEPS
  
A 4x4x4 LED Cube utilizes this code to run animations. It sets the 
Tmer1 prescaler to 1024 making it run at ~15kHz so that after ~15k 
events a second will have ellapsed.After a second an internal interrupt, 
ISR, is called to increment a counter variable. Instead of using millis()
to return times the program uses a function called millis_Overwrite to 
calculate times. Finally, instead of delay() a function named delay_Overwrite 
is used.

Layers are multiplexed so at most 16 LEDs are actually on at one time. The LEDs 
will dim if you turn them all on at once (quite a bit too). However, do NOT turn 
on all for LEDs in a column at once without multiplexing them. You could very 
likely damage your Arduino!

To write your own animations modify PatternTable. By setting a bit high,
  e.g. B0000 -> B0001 
A corresponding LED will be lit up. Which LED lights up depends on what pins are
wired to which LEDs. To modify this on the software end change the values of the 
colPins array and the layerPins array. 

If you wish to utilize Timer1 for anything be sure to delete the appropriate 
functions (and any reference to them):

    Timer1Init       - Delete
    ISR              - Delete
    millis_Overwrite - Replace with millis()
    delay_Overwrite  - Replace with delay()
    
To ensure better accuracy with the timer. Also if using the default functions 
some tinkering with the constants will be needed. LAYER _TIME and TIME_CONST 
would need to be changed 

A video of the cube can be found here:
  http://youtu.be/xqo9rBajY2Y
