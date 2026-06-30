# How to stream the lowest possible latency video from a DJI drone

## Intro
DJI Fly App is able to stream the video it is getting from a drone via RTMP protocol. 
We can stream from the app directly onto Youtube, but we can also stream to our PC where we can have more control over the stream.

## Prerequisites
You will need:
 - a DJI Avata drone and DJI Goggles 2 or similar
 - a mobile device with a DJI Fly App (this can only be downloaded from the DJI web site, the app is not present in the Google Play store)
 - an OTG USB Cable to plug into the Goggles and another USB-A-to-USB-C cable to plug the USB-A end into the OTG and USB-C end into into the device with the DJI Fly App
 - A network-connected PC with the following software:
  - VLC
  - OBS
  - MediaMTX
 - Both your PC and your Mobile Device should ideally be on the same WiFi network

## Stap 1 - Prepare for getting the video out of the DJI ecosystem
- Connect the Mobile Device with the DJI Fly App to your DJI Goggles, via the OTG USB Cable so you get the drone camera view in the DJI Fly App
- in a DJI Fly App once you are in the drone camera view
  - tap "..." menu in the top-right corner
  - tap "Transmission"
  - tap "Live Streaming Platforms"
  - tap "RTMP"
  - RTMP Address - here you will enter the address of your RTMP Server (later)
  - Stream Key - not necessary for us
  - Resolution - if we want low latency, set it to the lowest resolution - 720P
  - Bitrate - again, we want low latency, so we set this to "Smooth" 
- If your googles can connect to the phone by both cable and WiFi, use the cable option for faster video transfer. DJI Goggles 2 support cable connection only

DJI Fly App only allows to stream via RTMP protocol, and the app acts as a client, so we will need to setup an RTMP protocol server.
You can actually enter an address of a youtube RTMP protocol server here, for live streaming, but we're working towards having that video stream on PC for further processing. 

## Step 2 - setting up the RTMP server on your PC computer machine
This can be done in many ways, even with `ffmpeg` oneliner, BUT most of these ways introduce unnecessary latency and we don't like that. 
We will use the MediaMTX server, available from here: 
- https://github.com/bluenviron/mediamtx
- https://github.com/bluenviron/mediamtx/releases/tag/v1.19.2

Download the release zip, extract it, and run the `exe` file. 
Now, check your PC's IP address (Win+R, `cmd`, `ipconfig`)
Your MediaMX RTMP server works on `rtmp://YOUR_IP_HERE:1935`, so if your IP is `192.168.1.10` your RTMP server will be at `rtmp://192.168.1.10:1935`

## Step 3 - connecting the DJI Fly App to the server
We go back to the DJI Fly App "Camera View/.../Tranmission/Live Streaming Platforms/RTMP" window, as described in Step 1. 
We fill in the following options:
- RTMP Address: `rtmp://192.168.1.10:1935/live/` (with ending slash)
- Stream Key: `drone_video`
And we tap "Start Livestream"
Now we can on our PC open this url in the browser to see the WebRTC stream `http://localhost:8889/live/drone_video/` 

If everything works ok, you should see the feed from the drone in your browser tab.

## Step 4 - measure the video latency

To measure the delay from the drone camera to our screen we do the following: 
- Open https://www.mstimer.com/ on a half of your screen.
- Open the drone video feed on the other half.
- Point the drone at the mstimer.com website with the milliseconds counting. 
- Ensure the picture is clearly visibel in the drone video feed.
- Take a screenshot. 
- From a screenshot count the difference in millisecond between the time on mstimer.com website and the time on the drone feed
In our case that delay 


## Addendum
Test https://github.com/genymobile/scrcpy as well.
