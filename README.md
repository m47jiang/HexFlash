# HexFlash
A guide to flashing software onto arduino boards

Having trouble flashing software to your arduino boards? You've come to the right place :)

## STEP 1: Identify what you have on your hands
When flashing firmware to an arduino board, it's pretty important to know which board you have! Because different boards have different components on them so it doesn't matter how good your software if if your hardware doesn't support it :).

A good place to check out what your hardware can do is on the official [arduino](www.arduino.cc) website or also on [sparkfun](www.sparkfun.com). If you can't find your board there or any information on it... then it might not be an arduino compatible board or you need to find your information elsewhere... (that's some sketch arduino board your got there) 

## STEP 2: Flash most basic software on it
Now we made sure we have an arduino compatible board it's time to try flashing something onto the board itself.

- Download the [arduino IDE](www.arduino.cc/en/Main/Software) 
- Open an example project - Blink(this comes with the IDE)
	
![image of Blink](https://github.com/m47jiang/HexFlash/blob/master/blink_project.png)
	
- Select your board from tools -> board -> "your board here"
	
![](https://github.com/m47jiang/HexFlash/blob/master/select_board.png)

- If you can't find your board, using the Boards Manager to find it and install it
	
![](https://github.com/m47jiang/HexFlash/blob/master/boards_manager.png)

- Connect the board to the computer using usb cable
- Select the correct port from tools -> port -> "dev/ttyXXX" or "COMX" if no ports show up, you need to reset your board
- Once you've selected port, reset board again (usually there's a reset button on the arduino device)
- Compile and upload
	
![](https://github.com/m47jiang/HexFlash/blob/master/compile_upload.png)
	
- Congrats! You've just pushed your flashed your first board!
- If it didn't work (you see bad error messages), try the last 3 steps again (a few times)
	
## STEP 3: Flashing a .hex file from the command line
This step is for those that somehow got a .hex file from somewhere and want to flash it onto their boards. This method is probably not the most user friendly, so only do this if you're desperate.

Assuming that you've done steps 1&2 and have a xxxxx.hex file that is sitting around and you think it might solve your problems.   

- Open Arduino IDE and check "show verbose output during upload" in File -> Preferences
	
![](https://github.com/m47jiang/HexFlash/blob/master/verbose_preferences.png)

- Compile and push Blink or any other example
- Look at the ouput and try to find the line with 

	 	/{somepath}/bin/avrdude -C /{somepath}/etc/avrdude.conf -v -p atmega32u4 -c avr109 -P /dev/ttyACM0 -b57600 -D -U 
		 flash:w:/tmp/arduino_build_192428/Blink.ino.hex`

- Because we don't all have the same board, it is NORMAL to have slightly different text in the console
- All you need to do is copy this line and replace the last section
	
		flash:w:/tmp/arduino_build_192428.ino.hex`
	
- with

		{path_to_your_hex}/your_hexfile.hex
	
- DON'T FORGET TO HIT THE RESET BUTTON BEFORE RUNNING THIS LINE
- Run the changed result in the command line or terminal should look something like this:
	
	 	/{somepath}/bin/avrdude -C /{somepath}/etc/avrdude.conf -v -p atmega32u4 -c avr109 -P /dev/ttyACM0 -b57600 -D -U {path_to_your_hex}/your_hexfile.hex
