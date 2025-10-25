So we've added some configuration to the radio, namely 
- a model for our TinyWhoop, 
- then a timer to that, counting down from 3 minutes when armed, allowing us to roughly estimate how much battery power is left
- resettign the timer with the 6th S3 button
- Tuning the backlight with the S1 potentiometer
- Adding a SIM model with transmitter turned off to save battery power

We've experiences weird behaviors, like models not displaying, and ExpressLRS script not loading.
This seemed to work again after restart.

Turning on the radio few days later we've found some storage memory errors and RTC battery low warning. 

The battery change requires opening the radio, but the other errors, losing the names on models, all models having the transmitter turned off...
After a brief research, we concluded that the cause was a faulty connection to the SD card. We manually bent the metal on the card holder a bit, so it holds the card tighter.

Then we proceeded to try and save whatever is on the SD Card. During copying the contents, we had encountered an error. 
It had 3 directories named "LOGS". 

Some of our settings we could save, but it seems some MODELS and RADIO.yml settings were corrupted.

We decided to rebuild the contents of the SD Card using the factory dataset. 

First we got it from https://github.com/EdgeTX/edgetx, where the packs are included in the releases.
Since our radio had EdgeTX 2.8.4, we decided to download https://github.com/EdgeTX/edgetx-sdcard/releases/tag/v2.8.0
Radiomaster Boxer has 128x64 black and white display, so our target package was: 
https://github.com/EdgeTX/edgetx-sdcard/releases/download/v2.8.0/bw128x64.zip

Sadly, after upacking, we've found that there is no content in all the directories in here, as if this was just a skeleton of directory structure. 

We turned to Radiomaster, and have found this: https://radiomasterrc.com/pages/firmware
Where among others we have found `Boxer ExpressLRS 2.8.4 Factory SD Contents & Firmware`
This pack contains both firmware and default SD Card content, namely configs, sounds, etc. 

We've used the source pack and what was left of our corrupted SD Card, and after formatting it to FAT32, we've reconstructed the configs anew. 

These are mostly `.yml` files, so there was really no issue. 
One thing one needs to remember, after manually editing the RADIO.yml
you need to set the "manuallyEdited: 1" field, so it knows to re-generate the checksum for you.

So far, the radio has worked fine for a day. 
We heard it is advised to change the SD Card the radio came with for a better quality one. 
We will consider this if this one fails. 


