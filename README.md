from machine import Pin
import time
import neopixel

np = neopixel.NeoPixel(Pin(4), 16)


button = Pin(14, Pin.IN, Pin.PULL_UP)  

running = 0

while True:
    
    if button.value() == 0:
        time.sleep(0.2)          
        running = 1 - running
        while button.value() == 0:
            pass

    if running == 0:
        np.fill((0, 0, 0))
        np.write()
        time.sleep(0.05)

    else:
        for i in range(16):
            # allow stopping mid-cycle
            if button.value() == 0:
                time.sleep(0.2)
                running = 0
                while button.value() == 0:
                    pass
                break

            np.fill((0, 0, 0))
            np[i] = (0, 255, 0)   # GREEN
            np.write()
            time.sleep(0.1)
