# Home-Assistant-Weather-Station
Version 0.3 update!
____________________
-Added PMSA003i air quality sensor from Adafruit(i2c version).
  This version has issues with HA, namely it is difficult to get the SET pin to function correctly to set it to power off the laser and fan.  I was able to get it, but am still working on getting it to work reliably with a GPIO switch and interval: for automation.  As     of right now, everything is working, with the exception of the interval.  When I add the interval it works initially but fails to find the i2c device after restarts and cold boots.  I believe I need to add a way to store the i2c address to memory to prevent such a       thing...but ran out of time.
-Added a GPIO switch for restart of the entire ESP.
-Adjusted a few things.

AND personally I migrated from bread board to a proto board with solid soldered connections.  THIS drastically improved some glitches.

Pics will happen eventually.

I am going to need to create a custom badge for the dashboard because the air sensor using the defaults ones is janky af.  So hopefully that will be in the next update.  I also need to add an external antenna, once enclosed the ESP attenuation is crap.

----------------------
----------------------

Version 0.2
Incorporating a sparkfun style weather station kit into Home Assistant 

Hello, I struggled to find exactly what I needed to do this.  I based a lot of my initial tests off of several other configs with similar devices just not the 8 reed switch versions.  Added to that mix I found a lot of help just by sound boarding and bouncing ideas off of folks in the ESP8266/32 group on facebook.  I am sure people get tired of hearing about things I get stuck on but I am not terribly strong at programming without a little nudge.  With that said I give you...my creation.

Here is a picture of my current dashboard.  During this project I broke several files down inside HA because I thought the problem of reading only half the resistor values 4 of the 8, was caused by a config file.  SO I had reinstall, so it is a little sparce at the moment. But it WORKS!

![image](https://github.com/jumper-d-1981/Home-Assistant-Weather-Station/assets/80989663/a2f30459-399f-41fb-8543-9d352310b6f8)

As you can see I have no just the direction but also the angle.  Currently it will update every 5 seconds without fail, since my plan will be to hook this up in the field with a battery and solar panel...I see no issues with frequent communication.

The layout is simple enough.

DHT11 on pin 26
Speed Sensor on pin 36
Rain Gauge on pin 25
Direction Senson on pin 39

The Speed, Rain and Direction sensors are all in need of a voltage divider by the use of 3x 10k resistors I used 1/4 watt since it was what I had on hand.  This sounds complicated if you are not use to not relying on making your own stuff...and there are shields and board available but what is the fun in that?

Let us first connect 3.3V to one side of all three resistors, and the other side goes to the pins as mentioned(25,36,39), but also on the side of the pins jump over to the sensor's wire as follows.  In my case which is almost exactly like the spark fun weather station kits available for 79 bucks, there are 6 individual wires inside two cables.  The first cable has 2 wires, red and green.  Red to GND and green to divider.  The second cable has 4, both green and red goes to divider and black and yellow both go to GND.  Each resistor gets its own wire.  

I added the DHT11 like normal on pin 26.

That takes care of the setup I believe.
Now it looks like the resistance values vary wildly on some of these Direction sensors, mine were the right values in mixed up locations.  SO, be sure to run the example via an Arduino IDE before you jump into HA.  Same hardware setup as above will work fine...just adjust the pins in the code.

If that checks out and you device is working, let's now get it working in HA.  The full yaml is in the list above.  It should be more or less copy and paste, but you may need to comment some of it out to see clearly the LOG output of the sensors.  So you can read the value of resistance per direction, there are 8 total.  My values were very constant, but in the yaml you list a range, so I did .3 above and .3 below to give a little room for error.  List the directions and fill in the resistance per direction...create the range and apply it to your code.

It sounds more complicated than it is, but once you see the completed yaml it will make sense.

Okay, so go check the yaml.  And please be sure to GND properly.

Here are some more pictures.
![image](https://github.com/jumper-d-1981/Home-Assistant-Weather-Station/assets/80989663/901ddb09-e850-4e29-8b2c-88abf9465008)
The resistor values listed on this are bunk, like I said they were not accurate at all.
![image](https://github.com/jumper-d-1981/Home-Assistant-Weather-Station/assets/80989663/6bc3ceab-0b84-4c9e-ac7f-beab1e290d9d)
This is my breadboard of the mess, I should be able to get this small enough to fit along side the ESP into a small box.






