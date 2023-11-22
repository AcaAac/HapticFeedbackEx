# HapticFeedbackEx

This code allows for small Haptic Interaction with a PS4 remote controller.
In theory a PS3 remote controller with ERMs should work as well.

If the remote controller is not detected try installing SCP Driver to boot up PS controller to Windows software.

## Requirements

* Python 3.6+
* [Dualshock 4 Remote Controller](https://www.playstation.com/en-us/explore/accessories/gaming-controllers/dualshock-4/)
* [SCP Driver](


## Trigger Tresholds

You can play around with trigger tresholds and program each trigger to shoot and different input intensities:
```python
def get_trigger_values(controller):
    state = XINPUT_STATE()
    XInputGetState(controller, ctypes.byref(state))
    return state.Gamepad.bLeftTrigger, state.Gamepad.bRightTrigger
```

## Distance/Rumble Factor

The key snippet is integral to the haptic feel of the hardware:
```python
def set_vibration(controller, left_motor, right_motor):
    vibration = XINPUT_VIBRATION(int(left_motor * 65535), int(right_motor * 65535))
    XInputSetState(controller, ctypes.byref(vibration))
```