M5Stack M5Dial Timezones

This is a port of my [earlier repo ](https://github.com/PaulskPt/M5Stack_Atom_Matrix_Timezones).

Important credit:

I was only able to create and successfully finish this project with the great help of Microsoft AI assistant CoPilot.
CoPilot helped me correcting wrong C++ code fragments. It suggested C++ code fragments. CoPilot gave me, in one Q&A session, a "workaround" 
for certain limitation that the Arduino IDE has with the standard C++ specification. And CoPilot gave it's answers at great speed of response.
There were no delays. The answers were instantaneous! Thank you CoPilot. Thank you Microsoft for this exciting new tool!

Hardware used:

1. M5Stack M5Dial;

After applying power to the M5Dial device, the sketch sequentially will display data of six pre-programmed timezones.


For each of the six timezones, in four steps, the following data will be displayed:
   1) Time zone continent and city, for example: "Europe" and "Lisbon"; 
   2) the word "Zone" and the Timezone in letters, for example "CEST", and the offset to UTC, for example "+0100";
   3) date info, for example "Monday September 30 2024"; 
   4) time info, for example: "20:52:28 in: Lisbon".

Reset:

Pressing the button (of the display) will cause a software reset.

On reset the Arduino Sketch will try to connect to the WiFi Access Point of your choice (set in secret.h). If successful the sketch will next connect to a NTP server of your choice, then download the current datetime stamp.
If NTP is connected, the internal RTC of the M5Dial device will be set to the NTP datetime stamp with the local time for the current Timezone.
Next the sketch will display date and time of the current Timezone, taken from the external RTC, onto the OLED display. Every second the date and time will be updated.
Because the external RTC Unit has a built-in battery, the datetime set will not be lost when power is lost.

File secret.h:

Update the file secret.h as far as needed:
```
 a) your WiFi SSID in SECRET_SSID;
 b) your WiFi PASSWORD in SECRET_PASS;
 c) your timezone in SECRET_NTP_TIMEZONE, for example: Europe/Lisbon;
 d) your timezone code in SECRET_NTP_TIMEZONE_CODE, for example: WET0WEST,M3.5.0/1,M10.5.0;
 e) the name of the NTP server of your choice in SECRET_NTP_SERVER_1, for example: 2.pt.pool.ntp.org.
```
 In the sketch is pre-programmed a map (dictionary), name ```zones_map```. This map contains six timezones:

```
    zones_map[0] = std::make_tuple("Asia/Tokyo", "JST-9");
    zones_map[1] = std::make_tuple("America/Kentucky/Louisville", "EST5EDT,M3.2.0,M11.1.0");
    zones_map[2] = std::make_tuple("America/New_York", "EST5EDT,M3.2.0,M11.1.0");
    zones_map[3] = std::make_tuple("America/Sao_Paulo", "<-03>3");
    zones_map[4] = std::make_tuple("Europe/Amsterdam", "CET-1CEST,M3.5.0,M10.5.0/3");
    zones_map[5] = std::make_tuple("Australia/Sydney", "AEST-10AEDT,M10.1.0,M4.1.0/3");
```

 After reset the sketch will load from the file ```secret.h``` the values of ```SECRET_NTP_TIMEZONE``` and ```SECRET_NTP_TIMEZONE_CODE```, 
 and replaces the first record in the map ```zones_map``` with these values from secret.h.

Docs:

Monitor_output.txt

Images: 

Images taken during the sketch was running are in the folder ```images```.

Links to product pages of the hardware used:

- M5Stack M5Dial [info](https://docs.m5stack.com/en/core/M5Dial);
