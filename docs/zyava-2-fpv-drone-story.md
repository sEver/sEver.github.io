# Zyava 2 - 5" FPV drone build made from parts in 2025

// Document is a work in progress //

### Dictionary
- FC - Flight Controller - the circuit board 

1. Parts list
2. Build process
3. Software Config

    There are two ways to configure software on this drone. Either:
    - Connect the drone to a PC with a USB-C cable and use the [Betaflight Configurator](https://app.betaflight.com/)
    - Connect to the FC via Bluetooth with the [SpeedyBee App](https://www.speedybee.com/speedy-bee-app/)

    ##### The configuration process:
   
    1. Flashing Betaflight firmware
    2. Configuring OSD with DJI O3
    3. Configuring GPS
    4. Configuring Channels
    5. Configuring Modes
    6. Configuring Radio Control with DJI O3 and DJI FPV Remote Controller 2
    7. Checking direction of Motors
    8. Configuring GPS rescue - see https://betaflight.com/docs/wiki/guides/current/GPS-Rescue-v4-5

5. Test fligths checklist
    - Acceleromater Calibration executed at home by putting the drone on a definitely horizontal surface and pressing "Calibrate Accelerometer" button in the "Setup" tab of the SpeedyBee app.
    Rest of the steps executed in the field.
    - Drone tied to the end of a 20m long piece of strong string. The other end of the string tied to a heavy metal box used as a battery carrier.
    - The box and the drone placed 25m from the operator station as to put the operator outside of the range of the string, to prevent possibility of drone colliding with the operator.
    - Drone powered up by an USB-C connection to the FC port, from a portable Power Bank.
    - Android app `SpeedyBee` connnected to the FC via Bluetooth.
    - In the "Configuration" tab, "Magnetometer" switch switched to the "OFF" position. 
      As after looking at the heading indicated it was determined, that
      the GPS unit and the magnetometer in it are too close to both the motors and the battery power line to reliably detect magnetic north.
    - In the "GPS" tab confirmed that the GPS position fix is strong
    - In the "Failsafe" tab
      - Confirmed that the "Failsafe Switch" is set to trigger "Stage 2"
      - In "Stage 2 - Settings" section chose "Stage 2 - Failsafe Procedure" to "Land" with Throttle value 1100 
        and Delay for turning off the Motors during Failsafe [seconds] to `1.0` (This turned to be not so good idea later. See below.)
    - In "PID Tuning" tab "Rateprofile" sub-tab set "Throttle Limits" to `SCALE` and "Throttle Limit %" to `50`
    - Mounted standard 3-blade propellers "Ethix S3-WM-PC"

6. Test flights execution
    ##### Flight 0
    - Connected the battery to the drone, disconnected the USB-C power source from the SC
    - Confirmed the beeper button activates the beeper properly
    - Tried to arm the drone, got the "MSP" message as the reason for the drone not arming. To fix that, connected and disconnected the SpeedyBee app via Bluetooh
    - Moved the operator to a safe distance and armed the drone
    - Executed a take-off to an altitude of about 1.5m
    - Confirmed the controls work as expected
    - Used the "Failsafe" switch on the controller to trigger a failsafe. After a second drone just dropped into the grass
    - Drone Disarmed
    - Battery disconnected
  
    ##### Flight 1
    - Executed a short flight in goggles at an altitude of maybe 3-5 meters, determining that the Throttle value for a stable near-hover is around `44`.
    - Landed by disarming the drone at an altitude below 1m
    - Battery disconnected
    - Connected USB-C power source to the FC
    - In the SpeedyBee app in "Failsafe" tab set the "Throttle value used while landing" to `1440` (1000 + (44% * 1000))

    ##### Flight 2
    - Tested the Failsafe Landing by initiating it at an altitude of maybe 3 meters. After 1 second drone drops from the sky.
    - Determined that the "Delay for turning off the Motors during Failsafe [seconds]" is apparently determining how long the landing attempt will be ran before just disarming.
      This value needs to be set to give the drone sufficient time to land with the given throttle value from the essentially unknown altitude.
      That was determined to be a not so good Failsafe option.
    - In "Failsafe" tab
        - changed the "Stage 2 - Failsafe Procedure" to `GPS Rescue`
        - set the "Altitude mode" to `Current altitude`
        - set the "Initial climb (meters)" to `2`
        - set the "Throttle hover" to `1440`
        - set the "Minimum distance to home (meters)" to `10`
        - Saved the changes

    ##### Flight 3         
    - Disconnected the App
    - Connected the battery
    - Flew away from the starting point to a distance of around 17 meters
    - Initiated the manual Failsafe and GPS rescue
    - The drone climbed a bit and then circled around regardless of the wind and then landed properly near the starting point
        - This confirmed the GPS rescue worked properly

    At this point we determined it is safe to untie the drone from the tether. It was done.
    Further flights were executed in angle mode to first confirm proper operation at various ranges.
    The horizon and acro mode were also tested. 
      

     
