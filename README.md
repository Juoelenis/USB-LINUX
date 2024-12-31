When plugging in (almost) any USB device that device is by default handled by some builtin kernel module like usbhid, usb_storage,etc. In order to get this module to handle the device you must re-bind it to this module:

Fetch the name for the plugged in USB device

tree /sys/bus/usb/devices/
You may have to unplug and plug in the devices and run the above command a few times in order to find the correct name. The name should be in the format x-x:x.x

To find out what driver module is used for the current USB device use

usb-devices
Probably it will be usbhid

Unbind it from the current module

echo -n "x-x:x.x" > /sys/bus/usb/drivers/{DRIVER}/unbind
Bind it to this module

echo -n "x-x:x.x" > /sys/bus/usb/drivers/usb-test/bind
Verify with dmesg that the probe function in this module is reached

dmesg
