# BESSPIN-Demonstrator

```
This material is based upon work supported by the Defense Advanced
Research Project Agency (DARPA) under Contract No. HR0011-18-C-0013. 
Any opinions, findings, conclusions or recommendations expressed in
this material are those of the author(s) and do not necessarily
reflect the views of DARPA.

Distribution Statement "A" (Approved for Public Release, Distribution
Unlimited)
```

Cyberphysical demonstrator of BESSPIN technology

[![DARPA SSITH Automotive Demonstrator](assets/demonstator_with_people.jpg)](https://www.youtube.com/watch?v=ZgHQkOWEy1Q)

## Controls and Operation

TODO: elaborate on the experience

### Reset button
Reset button will reset the scenario back to the beginning.
![reset_button](assets/reset_button.jpeg)

### Emergency stop
Emergency stop button will cut power to the force feedback system. It is located in the glove compartment.
![emergency_stop](assets/emergency_switch.jpg)

### Functionality levels
The demonstrator has 3 functionality levels, and switches between them automatically to preserve as much functionality as possible in the presence of component errors.

1. Minimimal functionality
    - boot time: 2-3 min
    - simulator can be driven, but no hacks are possible
    - no SSITH technology is used
2. Medium functionality
    - boot time: ~5 min
    - only critical systems hacks can be executed
    - SSITH technology used to protect the ECU / critical systems (CHERI from SRI-Cambridge)
    - 3 FPGAs running
3. Full functionality
    - boot time: 15-20 min
    - all hacks and features are enabled
    - uses SSITH technology to protect the infotainment (HARDENS from LM), and the ECU / crirical systems (CHERI from SRI-Cambridge)
    - all 6 FPGAs running

## Exhibit setup

The car has a trailer jack for easy manipulation and staging. Once in place, the car is resting on the front supports and the back wheels. That way the front wheels can freely spin and steer, while the car is secure. For additional security add tire blocks around the rear wheels.

There are two latches hidden in the front grill that open the hood. 

1. Slide your finger behind the latch, and pull it open.
    ![right_latch](assets/right_latch.jpg)
2. Opened right latch
    ![right_latch_open](assets/right_latch_open.jpg)
3. Do the same for the left latch
    ![left_latch](assets/left_latch.jpg)
4. Now pop the hood cover and slide it towards you
    ![hood_cover](assets/hood_cover.jpeg)
5. Spin the trailer jack to lift and move the car, and then to lower it down in the exhibit location
    ![trailer_jack](assets/trailer_jack.jpeg)
6. The main power switch is located under the hood as well, as marked below. It is ON by default, but can be switched OFF to prevent accidental power up
    ![power_switch](assets/power_switch.jpeg)
7. Close the hood by reversing the steps above

## Power up

1. Plug the main power plug into the receptacle. A standard 15A circuit is sufficient. The actual peak power draw of the demonstrator is closer to 10A. If nothing happens after power up, make sure that the main switch (located below the hood as decribed above) is turned ON.
2. Power up the UPS device below the rear of the car - this device must be on to powers the LED strips
    ![led_power_button](assets/led_power_button.jpg)
3. Power up the steering wheel by pressing the small power button next to the emergency switch in the glove compartment. This should be done once Windows has booted, but before the simulator has started.
    ![steering_power_button](assets/steering_wheel_usb.jpg)
4. Center the steering wheel by rotating it until whe front wheels are aligned and the steering wheel is horizontal, as shown below.
    ![aligned_steering_wheel](assets/steering_wheel_alignment.jpg)
5. Connect a USB keyboard and a mouse. Press Alt+Tab to switch from the simulator into Windows desktop. On the bottom system tray is located steering wheel game controller software (stylized "F" icon) <a name="calibrate-steering-wheel"></a>
    1) Press the icon
    2) Select any of the two Fanatec steering wheel controllers and press `Properties`
    3) In the new window, go to the `Settings` tab
    4) Click on `Wheel Center Calibration`
    5) Click on `Yes`
    6) The steering wheel is now centered - bring the BeamNG simualtor into foreground, and press `Alt+Enter` to go back to full screen
    7) Disconnect the keyboard and the mouse
    ![centering_the_steering_wheel](assets/steering_wheel_centering.jpeg)
6. The LED lights will power cycle and change color a couple of times, until they start pulsing green.
7. The booted system looks like this:
    1. Green pulsing LEDs, simular running in self-driving mode
    ![nominal_front](assets/car_ready_nominal.jpg)
    2. Both hacker kiosk and CAN display running
    ![nominal_rear](assets/car_rear_nominal.jpg)
    3. CAN display shows no errors, and displays a live feed of CAN messages passed on the CAN bus
    ![nominal_can_display](assets/can_display_all_normal.jpg)
    4. Intial screen of the hacker kiosk looks like this:
    ![nominal_hacker_kiosk](assets/hacker_kiosk_nominal.jpg)




## Troubleshooting

### System health monitoring

The demonstrator has a health monitoring system, that warns the user in case an error is detected. This error is displayed in the small DEBUG window on the CAN display. Below is the debugging console on the CAN display showing MEDIUM functionality.
![debug_console](assets/debug_console.jpeg)

For more detailed view of the health monitor, `Alt+Tab` from the simulator to the terminal, and you will see a periodic summary of system health - ideally it looks like this:
![health_monitor](assets/health_monitor.png)

Note that some components are not monitored, and their status is marked as `UNKNOWN`. All log messages are printed on the console as well as saved into `C:\Users\galois\BESSPIN-Tool-Suite\besspin\cyberPhys\ignition\ignition.demonstrator.log`

### LEDs are off
Have you turned on the LED power source? It is the power button under the rear side of the car.
![led_power_button](assets/led_power_button.jpg)

### Steering wheel doesn't respond
Have you pressed the power button for the steering wheel force feedback system?
![steering_power_button](assets/steering_wheel_usb.jpg)

Note that even after that the simulator might not recognize the steering wheel controller, and the wheel might be off-center. Refer to the [Power up](#power-up) to see how to re-calibrate the steering wheel. Restarting the simulator/Windows PC might be necessary as well (but remember to power up the steering wheel *again* after the reset)

If the wheel still doesn't come up, open the hood and check if the light on the steering wheel hub is on.

- Steering wheel OFF:
    ![steering_wheel_power_off](assets/steering_wheel_power.jpg)
- Steering wheel ON:
    ![steering_wheel_power_on](assets/steering_wheel_powered_up.jpg)

### No sound
Sounds levels can be adjusted on the Windows PC - attach a keyboard and a mouse to the USB hub in the glove compartment, press `Alt+Tab` to escape the simulator, and adjust the sound volume accordingly.

### Infotainment doesn't work / No music
First, check the CAN display for any errors. The infotainment/music works only in [Full Functionality](#functionality-levels) mode.

If no errors are displayed, make sure you are in manual mode (can drive the car) and press volume/music station button.

The last resort is to check the [System health monitoring](#system-health-monitoring) to see if there are any errors in the infotainment backend.

### Cannot shift into Park
The ignition key might be in the OFF position. Rotate the key and move the shifter to find the correct key orientation.
![ignition_key](assets/ignition_key.jpeg)

### Component failure
If there is a component error, the demonstrator tried to resolve it by restarting the component where possible. However, an automatic reset is not always possible, in which case an error message will be shown on the CAN display. 

Usually the best course of action is to [power cycle](#power-up) the whole demonstrator and that should resolve most of the problems.




## Known issues

Because the demonstator uses experimental components, there are some known issues that might pop up.

![emergency_stop_button_in_detail](assets/emergency_switch_detail.jpg)

### Beamng reset
[PyBeamng](https://beamngpy.readthedocs.io/en/latest/index.html) and [BeamNg](https://beamng.tech/) occassionally loses connection to the rest of the demonstator. Usually we can reconnect within a couple of seconds, but during that time the driver might lose control of the vehicle. In the worst case, an Ignition error is displayed on the CAN display and in such case the demonstrator (or more specifically the Ignition component) has to be restarted.

### Steering wheel not centered after a restart
The [Fanatec podium wheel base](https://fanatec.com/us-en/racing-wheels-wheel-bases/wheel-bases/podium-wheel-base-dd1) does not keep its center calibration, and as a result is not perfectly aligned after a restart. This seem to be a Fanatec driver issue. To re-calibrate the steering wheel, please follow the [calibration procedure](calibrate-steering-wheel)

### LEDs get stuck
Sometimes a segment of the LEDs get stuck in a given color/pattern. The only known remedy is to power cycle the demonstrator (more specifically restart the ignition subsystem, which manages the LEDs).


