# Anycubic-Predator
Configuration File

As many people that've bought an Anycubic Predator with the Trigorilla-pro Board I also had the problem with the default e-steps and a circulating hotend temperature. In my case the extruder extruded 96mm instead of 100mm at a temperature of 210°C and the Hotbed temperature circulated between 200 and 220°C which made printig nearly impossible due to the reason that the printer was waiting for a kind of constant temp to start... which never happened.

After searching the net what to do, most people decided to change the mainboard to a Duet or an SKR v1.3 and so will I. But I wanted to give it a try at first.
So I found out that the board is made by chitu and that they are using different g codes!

User rq3 postet at Thingiverse that it is possible to change the configurations as you can read at the following link:

<a href="https://www.thingiverse.com/groups/anycubic-predator/forums/general/topic:40393#comment-2752705">Tweaking the Anycubic Predator</a>

Sounded well, but even trying those commands using pronterface didn't change anything. I was able to start AutoPID and got new values, but the temps were still circulating. And changing the e-steps also had no effect.

But what worked was:

1.  connect your Predator via USB and start pronterface

2.  type in the command:  M8512 "Configuration_file.gcode"  - now your printer writes a file named Configuration_file.gcode 
    to your SD card which should already be inserted to the Printer.

3.  save this file for backup!!!!

4.  open the file with a texteditor

5.  go to the command 8011... there you can change your e-steps. A lower value raises the steps and a higher value decreases     the steps. User ROB5251 at Thingiverse wrote a calculator for the correct e-steps. You can find it at:

    https://docs.google.com/spreadsheets/d/1VOz1dg8I2bXwsOWCdKM_GWCrxGOX-A2hQ6pdoTR2gPw/edit?usp=sharing
    
    For me, with the original Titan clone, a value of S0.00235 worked fine (at 210°C with mounted bowdentube)

6.  scrolling down in the file you will find the command M301 (which should sound familiar if you know Marlin)
    Here I used P15.650000 I0.1 D62.879997 which I also found out via trial&error and the following explanation found at 
    
    https://reprap.org/wiki/PID_Tuning:
    
    For manual adjustments:
    if it overshoots a lot and oscillates, either the integral gain needs to be increased or all gains should be reduced
    Too much overshoot? 
    Increase D, decrease P.
    Response too damped? Increase P.
    Ramps up quickly to a value below target temperature (0-160 fast) and then slows down as it approaches target (160-170) 
    slow, 170-180 really slow, etc) temperature? Try increasing the I constant.

7.  Now you save the file to your SD, insert it to the printer and hit print.

8.  After 2-3 seconds the printer will write finished in the display and your values are changed. If you mess up anything you     can always use your backup config gcode file to get the standard presets back!

At the following Link you can find much more commands to change for your needs

http://www.customize-3d.com/chitu-g-code-explained.html

Feel free to try the file I created or make your own and be happy beeing able to use the original mainboard!

P.S. This is my first time making a git, so if any of the people whose links I used doesn't want me to do so, please contact me ;)
