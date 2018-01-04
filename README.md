# retroidle
Retroidle is a Linux bash script that runs commands when GPIO interrupts have been idle for a set time.

It watches /proc/interrupts for changing pinctrl interrupt counts.

I created it for use with retropie and Adafruit's retrogame to control a marquee light relay on my Donkey Kong arcade cabinet.

I rebuilt a Donkey Kong arcade using a Raspberry Pi 3 running RetroPie. The arcade controls are attached to the GPIO inputs. AdaFruit's retrogame is used to emulate keyboard inputs from the GPIO. 

A relay module is connected to a GPIO output and controls the marquee lamp. That way I can leave the pi running and have it automatically turn the marquee off and on when the arcade isn't in use.

When the arcade controls haven't been used for the number of seconds set by the idle_max variable the script runs a command to turn off
the marquee relay. When a button is pressed or the joystick moved the pinctrl interrupt counts change and the relay is turned on.

The script can be used with any interrupt by changing the awk search pattern.

Change the idle_max value to the number of seconds of no interrupts that you want before the idle period starts.

Add your commands to be executed when the idle period starts in the idle_start subroutine.
Add your commands to be executed when the idle period ends in the idle_end subroutine.
The idle_while subroutine runs once a second while idling. I use it to blink an LED attached to a GPIO pin under the arcade control panel.

The idlecount variable is reset to idle_max every loop during idle to prevent overflow. 

I put retroidle in /usr/local/bin and run it from /etc/rc.local. Put an & after the command to run it in the background.
/usr/local/bin/retroidle &

Happy gaming!

Alan
