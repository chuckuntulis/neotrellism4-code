# neotrellism4-code
Working to debug some ongoing problems
Here is my first attempt at isolating the problem:

The following are a few snippets of code because I am not sure what I need to include. If I need to put my full code in Github, let know and i will learn how to do that and pass on the pointer.



In Mu, I do a Save and the Neotrellis lights up. When I depress any key on the Neotrellis M4 the lights extinguish I get the following "Error reported in the REPL" 

--------------------------------------------

Traceback (most recent call last):

  File "code.py", line 154, in <module>

  File "adafruit_hid/keyboard.py", line 100, in press

AttributeError: 'int' object has no attribute '_add_keycode_to_report'



Press any key to enter the REPL. Use CTRL-D to reload.

------------------------

my code snippet follows ...originally from John Park. It worked fine up until I had the problem that danh helped me with. I was able to load what I think are the recommended libraries and the Neotrellis worked. The only changes to the code were to change kbd = Keyboard from kbd = Keyboard() and 

cc = ConsumerControl from cc = ConsumerControl()

to get the code to not complain about the kbd and cc. I assume because the newer versions that I loaded into lib on the CIRCUITPY device



from board import SCL, SDA
import adafruit_trellism4
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keycode import Keycode
from adafruit_hid.consumer_control import ConsumerControl
from adafruit_hid.consumer_control_code import ConsumerControlCode

...

99      for keycode in keycodes:
100        self._add_keycode_to_report(keycode)

101    self._keyboard_device.send_report(self.report)

-------------------------------

Looking at the code in https://github.com/adafruit/Adafruit_CircuitPython_HID/blob/master/adafruit_hid/keyboard.py, I see the following:

153           if keymap[down][1] == KEY:
154                kbd.press(*keymap[down][2])
155            else:
156                cc.send(keymap[down][2])

-------------------------------

but I do not understand the error message about 

  File "adafruit_hid/keyboard.py", line 100, in press

AttributeError: 'int' object has no attribute '_add_keycode_to_report'

