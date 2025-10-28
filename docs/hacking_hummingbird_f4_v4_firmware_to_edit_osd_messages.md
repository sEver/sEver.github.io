# `Hummingbird F4 V4` Tinywhoop drone comes with some 'funny' messages in its OSD and we will show you how to get rid of them

## The drone runs Betaflight 4.5.1, but it's not built from the official repo, but from NewBeeDrone's fork of Betaflight

The v4.5.1 release of this fork can be found here: https://github.com/newbeedrone/nbd-betaflight/releases/tag/v4.5.1

The owner of NewBeeDrone, Kelvin, [stated](https://www.youtube.com/watch?v=sUkdtgbjXl0&t=1441s
) that the custom firmware was necessary, because Betaflight refused to include anything not-hardware related in the hardware target configs like this one: https://github.com/betaflight/config/blob/main/configs/HUMMINGBIRD_AIO255/config.h

With the custom firmware, NewBeeDrone is therefore able to add any and all Betaflight changes they needed to add to the drone. 

It seems that among these changes added to the NewBeeDrone firmware binary, are also these OSD messages:

"SEND IT"
"BLAH BLAH BLAH"
"OH SHIT RSSI LOW" 
"BATTERY DYING"
"DAMN HOT %c"
"DAYUMN"
"> SHAME BRO <"

Which are replacements for the messages originally stored in here, among others:  
https://github.com/newbeedrone/nbd-betaflight/blob/v4.5.1/src/main/osd/osd_warnings.c

We presume the replacements were included in the build by overriding the code from `osd_warnings.c` with something stored in the `/src/main/config` directory, which is added to `.gitignore` file in the `nbd-betaflight` fork and therefore is not uploaded to the repo.

Since we don't know what other important changes were added to the build in that way, we decided to not attempt recompiling the firmware from the incomplete source, but instead to take a look into the compiled `.hex` firmware file provided for download on the `releases` page.

The file in question is: https://github.com/newbeedrone/nbd-betaflight/releases/download/v4.5.1/betaflight_4.5.1_HUMMINGBIRD_F4_V4_d7ea36269.hex
It contains rows of HEX data written in plain ASCII, as so: 

```
...
:10757000465245450044414D4E20484F5420256316
:107580003A202533642563002020444159554D4E4F
:107590002020005243534D4F4F5448494E47004F0F
...
```

This is known as [`Intel HEX`](https://en.wikipedia.org/wiki/Intel_HEX) format.

We can try to look in that data for one of the messages, namely, let's try with 'DAYUMN'.

We convert this message to HEX first:
```
ASCII |  D  A  Y  U  M  N
HEX   | 44 41 59 55 4D 4E
```

and without spaces that hex string is `444159554D4E`, which can be found in the part of the file quoted above. 

We've written a simple python script to convert the entire firmware file to ASCII and confirm that all the messages are in there. 
What was left is to come up with a way to edit them in a comfortable way, without damaging the binary parts of the firmware file. 

This might not be trivial, as this `Intel HEX` file contains not only representation of raw data in ASCII HEX representation, but also contains metadata, and, most importantly - a checksum for every line, which we will have to recalculate after changing the contents. 

So we've coded a pair of scripts, to convert the HEX file into a JSON with separate record for every line from the HEX, as 
converting the HEX to just plain ASCII was not a viable method (we were losing the information on where the HEX data lines ended).

To confirm the scripts work as intended, we've converted the original firmware to an "Editable JSON" file, and then, we converted that file back to Intel HEX, when we confirmed that the resulting file was identical to the initial one.

Because we're not going to mess with any pointers referencing the addressess of these strings in firmware memory space, we're going to edit the messages without changing their length.

And so we changed

`SEND IT` to
` READY `

`OH SHIT RSSI LOW` to
`WARNING RSSI LOW`

`BATTERY DYING` to
`BATT CRITICAL`

`DAMN HOT` to
`CORE HOT`

`  DAYUMN` to
`BATT LOW`

`> SHAME BRO <` to 
`> TURN OVER <`


Sadly, we weren't able to determine what was the original message for the 
"BLAH BLAH BLAH" replacement in NewBeeDrone's version of betaflight, so this one message was omitted in our cleanup.

After editing the messages, the payload was re-encoded into an Intel HEX file again.

The drone was connected via USB to a PC Computer, a backup of the settings was made, and the `betaflight_4.5.1_HUMMINGBIRD_F4_V4_CLEANED.hex` firmware was flashed onto the drone. After the flash, the backup of the settings was restored and drone was flown for 2 packets, to confirm all the messages look like intended. 

The resulting firmware file is available for download here: [betaflight_4.5.1_HUMMINGBIRD_F4_V4_CLEANED.hex](https://github.com/sEver/Betaflight-4.5.1-for-Hummingbird-F4-V4-with-OSD-messages-CLEANED/releases/download/v4.5.1-CLEANED/betaflight_4.5.1_HUMMINGBIRD_F4_V4_CLEANED.hex)

And the tools used in the process are also available in this repo: 
https://github.com/sEver/Betaflight-for-Hummingbird-F4-V4-with-OSD-messages-CLEANED

