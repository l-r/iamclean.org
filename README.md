# iamclean.org

I've decided to port this here for archival purposes. The website iamclean.org does not actually exist anymore.

Please note, the code was written in 2007 (it's old!).

![Alt text](/finished.jpg "Optional title")

## From the original website

It was pretty difficult to find any documentation on how do send data to a remote server or php page using an Xport from Lantronix and an Arduino together, it seems like the only person on the net to have used it the Xport a lot is Tom Igoe and his students at NYU (documented anyways). Most of the examples on their pages deal with communicating with the Xport from the net, and not the other way around. This made my life a whole lot more difficult, and Marc and I ended up staying up about 35 hours in a row to figure this out in time. Iit proved to be very simple in the end, the code is very concise. With that said, I am very open to questions or interrogations if you have any, I've played around a lot now with the xPort and the Arduino and I definitively want to encourage people to work with these. This is my email.

**Data circulation**
So this is basically how the data flows...from the docking station to the Arduino, to the xPort, to the PHP page, to the mySql database. When the visualisation is requested, a php page compiles all entries in the database, generates a new xml file and embeds the new flash file, which reads off that xml file.

**Hardware list**
  * Arduino Diecimila
  * Lantronix xPort
  * 1 green led
  * 1 IR (infrared) emiter and receiver (to create a switch)
  * wires
  * 10k resistor
 
**Software**
  * You'll need the Arduino software of course to upload to it...
  * Device installer from Lantronix
  * Telnet (MacTerminal on Macs?), free on all windows. For testing mostly.

**Before starting with the arduino**
  * Don't foget to plug your digital 3 (arduino) to the xport reset pin (should be 3 also)
  * In this example, the "button" variable is just a value to activate the switch.
  * Don't forget to substitute your page and domain. the http:// is not necessary.

**Xport settings**
 
->Channel 1
Baudrate 9600, I/F Mode 4C, Flow 00
Port 10001
Remote IP Adr: XXX.XXX.XXX.XXX, Port 80 
Connect Mode : c5
Disconn Mode : 00
Flush Mode : 00

->Expert
TCP Keepalive : 45s
ARP cache timeout: 600s
High CPU performance: disabled
Monitor Mode @ bootup : enabled
HTTP Port Number : 80
SMTP Port Number : 25
 
***important notes***
  * Remote IP address : thats the address of your server. You HAVE to fill it in. because...
  * Connect mode C5 is auto-connect. which means as soon as the xPort is booted, it will connect to your server IP address.
  * Port number should be 80.


***Suggested steps to get stuff working***
1) Wire everything up, make sure you power the Arduino via an external source (more consistent readings)
2) With the device installer, make sure your computer can read the xPort on the network (connect it into your router)
3) Power from the Arduino -> Power of xPort (pin 2), Ground Arduino -> Ground xPort (pin 1), RX to TX and TX to RX
4) Get your Arduino to talk to telnet and vice versa using this simple example from Tom Igoe
5) When they can talk back and forth, open Telnet and try executing your page though it. When it works, you know what you need to send from the Arduino to the Xport to make it execute.
6) Run from your Arduino, and the xPort should send the data out without anything else.
 
I know I've skipped a lot of little steps, but that's the bulk of it.
 
***Other references you might want to check out***
http://itp.nyu.edu/~yc581/blog/115
http://blog.faludi.com/2005/11/23/xport-twins/
http://www.tigoe.net/pcomp/code/category/category/circuits/lantronix