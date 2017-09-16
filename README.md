![GitHub Logo](/doc/media/Grbl Logo 250px.png)


***

Grbl is a no-compromise, high performance, low cost alternative to parallel-port-based motion control for CNC milling. It will run on a vanilla Arduino (Duemillanove/Uno) as long as it sports an Atmega 328. 

This project is to port the Uno code to other Arduino boards like the Leonardo, PRIMO and the Gerbil K40 Controller which hosts a 328PB-AU.
The main purpose is to use these boards is to drive robots and in my case the K40 chinese laser cutter so it can use g code based open software like inkscape.

The controller is written in highly optimized C utilizing every clever feature of the AVR-chips to achieve precise timing and asynchronous operation. It is able to maintain up to 30kHz of stable, jitter free control pulses.

It accepts standards-compliant g-code and has been tested with the output of several CAM tools with no problems. Arcs, circles and helical motion are fully supported, as well as, all other primary g-code commands. Macro functions, variables, and most canned cycles are not supported, but we think GUIs can do a much better job at translating them into straight g-code anyhow.

Gerbil specific: The code has been optimised to run CO2 tube type lasers which require a low pwm frequency (between 60 and 300 Hz) in contrast with aluminium RF excited lasers which run on higher freq. between 5kHz and 20kHz. Higher frequency gives more accurate high resolution engravings but lack in gray shades. Low frequency gives lots of grey shades but lacks in resolution and is a slow process!

Gerbil has a specific command to select the pwm mode $28:
- 0 default mode: 244 Hz (best for CO2 tubes high voltage driven gas)
- 1 low resolution mode: 61 Hz fast pwm
- 2 high resolution mode: 1.9kHz fast pwm
- 3 highest resolution mode: 15kHz (synrad rf excited lasers etc) fast pwm
- 4 122 Hz phase and freq correct pwm
- 5 1kHz phase and freq correct pwm
- 6 7.5kHz phase and freq correct pwm

Engraving speed between 700 and 1200mm/min gives the best results. Above these speeds, the pwm is too slow to keep up with the engraving.

grbl/doc contains the inkscape engraving and cutter plugins (just drop the .py and .inx in inkscape/share/extensions folder on your MAC or PC)
grbl/doc/script contains a simple streamer script 'stream.py' to stream big files to Gerbil.

Grbl includes full acceleration management with look ahead. That means the controller will look up to 18 motions into the future and plan its velocities ahead to deliver smooth acceleration and jerk-free cornering.

* [Licensing](https://github.com/grbl/grbl/wiki/Licensing): Grbl is free software, released under the GPLv3 license.

* For more information and help, check out our **[Wiki pages!](https://github.com/gnea/grbl/wiki
