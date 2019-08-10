# pydeconz
Homeautomation Library for the tech savvy (depending on zigbee/deconz-rest)

__This should be a library to easily build home automation scripts on top of the deconz-rest api__
It can be used to easily issue comands to devices connected to deconz, subscribe to events and mix the two.
For example: on motion -> switch light on

### Sample Code

<code>
from pydeconz.Router import Router
router = Router()
##
# print some objects
##
sensors = router.getAllSensors()
for s in sensors:
    s.println()
print("---")
lights = router.getAllLights()
for l in lights:
    l.println()

# subscribe to websocket (for updates)
router.startAndRunThread()

#get motion sensors
bewegungsmelder = router.getSensorsByIcon("🏃‍♂️")

def onMotion(sensor, key_that_changed, oldval, newval):
	print("somebody moved - or stoped moving")

bewegungsmelder[0].subscribeToAttribute("state_presence", onMotion)

</code>