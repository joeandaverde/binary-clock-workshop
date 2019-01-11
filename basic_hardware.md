# Basic Hardware

During this lab, you will start attaching external hardware such as LEDs and controlling using the Python programming language. 

## Wire Up LED

1. Add LED (green) to breadboard with netative (shorter) leg in G30 and the positive (longer) leg in G29.
1. Add a short black wire connecting J30 to closest negative (-) row.
1. Ground the negative row by connecting a long black wire to the top negative (-) row hole around J1 to a Ground on the Raspberry Pi.
1. Add a color wire from J29 to GPIO 21.

## Controlling LED

1. On the Raspberry Pi command-line, start interactive Python shell.
```
python3
```
2. Initialize the LED GPIO.
```
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(21,GPIO.OUT)
```
3. Turn LED on.
```
GPIO.output(21, GPIO.HIGH)
```
4. Turn LED off.
```
GPIO.output(21, GPIO.LOW)
```
5. Impport time library.
```
import time
```
6. Blink LED.
```
while True:
    GPIO.output(21, GPIO.HIGH)
    time.sleep(1)
    GPIO.output(21, GPIO.LOW)
    time.sleep(1)
```

NOTE: The while True creates an infinate loop for all code indentened after it.

7. Watch LED blink for a minute or so.
8. Ctrl+C to terminate loop.
9. Exit Python interactive shell.
```
exit()
```

## Gpiozero Library

Having to manage the GPIO port can be a hastle in more complicated programs. The Gpiozero Python libary simplifies this.

Documentation: https://gpiozero.readthedocs.io/en/stable/

### Install Gpiozero and Git

1. On the Raspberry Pi command-line run:
```
sudo apt update
sudo apt install git python3-gpiozero
```

### Controlling LED with Gpiozero

1. On the Raspberry Pi command-line, start interactive Python shell.
```
python3
```
2. Initialize the LED GPIO.
```
from gpiozero import LED
led = LED(21)
```
3. Turn LED on.
```
led.on()
```
4. Turn LED off.
```
led.off()
```
5. Blink LED.
```
led.blink()
```
6. Blink LED faster.
```
led.blink(.1, .1)
```
HINT: https://gpiozero.readthedocs.io/en/stable/api_output.html

7. Blink LED slowly 3 times.
```
led.blink(2, 2, 3)
```
8. Exit Python interactive shell.
```
exit()
```

## Morse Code Script

Create a morse code script that blinks ...---... or short short short long long long short short short repeat.

1. On the Raspberry Pi command-line open a new morse.py file using the nano text editor.
```
nano morse.py
```
2. Add the following Python code.
```
#!/usr/bin/env python3

import time
from gpiozero import LED

led = LED(21)
while True:
        led.blink(.5,.5,3, False)
        led.blink(1,.5,3, False)
        led.blink(.5,.5,3, False)
        time.sleep(5)
```
3. Exit nano using Ctrl+X.
4. Make script executable.
```
chmod 744 morse.py
```
5. Execute script.
```
./morse.py
```
6. End script with Ctrl+C.