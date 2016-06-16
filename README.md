#This is a development branch for CYCLOP+. The latest release is in the Master Branch

#CYCLOP+
##Introduction and Goals
The first goal of this project (CYCLOP+) is to add the ability to manually select channels using only the standard button on the receiver of the Quanum Cyclops.
The second goal is to add support for connecting an OLED display to the receiver so that more information can be presented.
No hardware alteration is necessary to use CYCLOPS+. The OLED display is optional.

##Words of Warning
The project is in an early stage and use of the FW is completely on your own risk.
To install the firmware you remove the receiver from the googles and program it using a ISP programmer. It is possible to destroy the receiver electronics if you connect VCC (the +3.3volt wire comming from the programmer) to the wrong pin. Other types of wiring errors will lead to the programmer not working, but will not destroy anything. Always double check that VCC is connected correctly before you turn on power.
It is possible to "Brick" the processor in your receiver by tampering with the so called processor fuses. There is no need to change any fuses from their original values (0xE2 0xD9 0x07). Leave them alone.

## Modify the Hardware (optional)
- Solder a 2x3 block of pin headers into the ICSP port. This is found just under the button switch. The pins should point upwards on the same side as the receiver tin can is installed. The top right pin is VCC. If you do not want to solder anything you can program the boad by temporarily pushing programming pins into the PCB ICSP connector holes and program the board.
- Connect a 128x64 OLED screen with I2C interface to the I2C pins (Ground, VCC, SCL, SDA). There are several pads available on the board, so you do not have to solder to the processor legs. The board designer was kind enough to add three pads just above the display contact that are (from the top) Ground, SCL and SDA. The OLED screens can use either 3.3 or 5 volts for VCC. I used 5 volts. The easiest point to find this is on the lowest pin on the main display contact. My 5v feed was calibrated to 6.15 volts. You might want to adjust this if you use 5 volt. Please note that the pads on the back of the board marked SCL1 and SDA1 are mislabeled. They should be swapped. 

##Build CYCLOP+ (optional)
- The project is built using the Arduino development environment. Download the Arduino development environment from www.arduino.cc.
- Install the development environment.
- Download the CYCLOP+ source code from GitHub.
- Navigate to the cyclop_plus.ino file and open it in the Arduino development environment.
- Download the two external LCD libraries (Adafruit GFX and Adafruit SSD1306). This is done within the Arduino environment. 
- Specify "Arduino Pro or Pro Mini" as board. Then select "Atmega 328 (3.3 volt, 8 MHz)" as processor. These settings are found in the "Tool" menu.
- Build the project by pressing the v icon in the upper left corner of the Arduino window.

##Load CYCLOP+
- Build CYCLOP+ or download the latest stable version of CYCLOP+. The firmware file is called cyclop_plus.hex and can be downloaded from this page (right-click and download): https://github.com/Dvogonen/cyclops_plus
- To upload the sketch to the receiver board you must have an ISP programmer for AVR micro controllers. The original is called AVR ISP mkII and is expensive. The design is open source and copies can be had for around 20$. But there are several other cheaper alternatives available to choose from. An USBASP is the cheapest alternative (2-3$). If you decide to get a USBASP, make sure to select one that can be switched between 3.3-volt and 5-volt output. You can also build your own using an Arduino that has a USB interface, such as a One or a Nano. Build instructions are easy to find if you google around.
- Install the drivers for the programmer. These are sometimes difficult to get to work. Be prepared for a bit of a fight and use google a lot. Google is your friend. For the USBASP driver you may have to use a helper program called Zadig to install the driver.
- Configure the ISP programmer to use 3.3 volts.
- The actual programming is done with a program called AVRDUDE (seriously). This is command line tool and is horrible to use. But there is a GUI version available called AVRDUDESS that is quite nice. You find it here: http://blog.zakkemble.co.uk/avrdudess-a-gui-for-avrdude/
- Start AVRDUDESS. Select your ISP programmer in the Progrmmer box. Select the type of MCU (Atmega 328p). Select your CYCLOP+ firmware file in the Flash box and execute a write.
- If everyting is set up correctly the LED on the receiver board next to the ISP pin header will light up for a minute or so. When it goes black again the porogramming is done and the board can be mounted in the googles.

##Use CYCLOP+
- A single click jumps up in frequency to the closest channel among the 40 available.
- A double click jumps down in frequency
- A long click (0.6 - 2 seconds) triggers a autoscan for the best channel, just like a single click does in the original firmware.
- A long-long click (> 2 seconds) triggers a manual frequency scanner. The receiver will start cycling through all channels quickly. Hold down the button again when the channel you want to use flickers onto the main display.

####License
The MIT License (MIT)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.