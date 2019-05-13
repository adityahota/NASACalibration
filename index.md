# Improving the Measurement of Reaction Time Tests on Windows Laptops
ESE 350 Final Project, Spring 2019

[Aditya Hota](https://github.com/adityahota) and [Lakshay Sharma](https://github.com/lakshay2010sharma)

In collaboration with [Dr. Mathias Basner, University of Pennsylvania School of Medicine](https://www.med.upenn.edu/uep/faculty_basner.html)


## Week 5: Public Demo
**May 10, 2019**
Before the public demo, we had a chance to demo our product to Dr. Basner and test it out on multiple other laptops, three of which were the same model that was newer than the one we had been using. This gave us a chance to collect and analyze four times the amount of data we previously had, with the bulk of it coming from keyboards of much higher quality. We ran the calibration plan as before, and in addition to mean and standard deviation, we calculated other statistical information such as 95% confidence intervals and 95th percentile. We also plotted a scatter plot of the values obtained, as well as a histogram, that greatly helped in visualizing the trends in the data, the precision in the calibration setting for the spacebar used and the quality of the keyboard. The appropriate graphs and tables are shown below:

![Data Table](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Data_Table.png "Data Table")
![Laptop 1 H](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_1_Hist.png "Laptop 1 H")
![Laptop 1 T](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_1_Plot.png "Laptop 1 T")
![Laptop 2 H](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_2_Hist.png "Laptop 2 H")
![Laptop 2 T](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_2_Plot.png "Laptop 2 T")
![Laptop 3 H](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_3_Hist.png "Laptop 3 H")
![Laptop 3 T](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_3_Plot.png "Laptop 3 T")
![Laptop 4 H](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_4_Hist.png "Laptop 4 H")
![Laptop 4 T](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Laptop_4_Plot.png "Laptop 4 T")
![Mouse 2 H](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Mouse_2_Hist.png "Mouse 2 H")
![Mouse 2 T](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Mouse_2_Plot.png "Mouse 2 T")


In addition, we also did the same process for mouse clicks, since a user in *Cognition* can provide his reaction using either the spacebar or a physical left mouse click button. The data obtained showed that the mouse click not only has more variability for the calibration delay, but also changes significantly based on the center of the actuation force. Therefore, the mouse click is a significantly worse method of input compared to the spacebar on the laptops tested, as far as calibration delay is concerned.

## Week 4: Reach Demo
**May 3, 2019**
For the reach demo, we focused on three main aspects of the project: data analysis, stress-testing under CPU/GPU loads and packaging of the final product.

The data analysis was done by running *Cognition* on the given test laptop and using the solenoid to act as a perfect human so that the values given by *Cognition*, minus the delay found using the pressure sensor gives us the required calibration value for each press. The fifty values obtained from a full 3-minute calibration plan in *Cognition* were then used to find the mean and standard deviation for the desired calibration delay. The mean obtained for the test laptop used was around 36.29 milliseconds, with a standard deviation of 3.24 milliseconds.

For stress-testing, we used a program called *CPUSTRES* to generate artificial CPU or GPU loads as desired, and the effect of this on *Cognition* values was observed. We found that there was absolutely no effect on either the mean or the standard deviation in the values obtained at any level of load possible, ranging from 0% to 99%. At 100% CPU load, we found that sometimes the light would flash in *Cognition* and the solenoid would consequently actuate, but *Cognition* would not read the value, thereby implying that the high background load prevents *Cognition* from getting the maximum number of values it can get, but this only affects the size of the sample space obtained, and still has no effect on statistics. This is to be expected, because *Cognition* was designed to be resistant to background loads by acquiring a very high priority when the application is started. Thus, our solution held up to the stress tests.

For final packaging of the product, we attached male barrel jack headers to the ends of the wall wart used to power the solenoid, the solenoid itself and the other power supplies used. We then soldered female barrel jack headers to the appropriate places on the protoboard, to remove the need for careful positioning of wires entirely. Then, we designed an acrylic box for the whole setup in Solidworks, laser cut the plates and screwed the box around the protoboard, with appropriately-sized holes snapping around the wires for the female barrel jack headers. This completed the black-box setup that is user-friendly as well as idiot-proof.
![Finished Box](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Box_Fixed.JPG "Finished Box")

## Week 3: Baseline Demo
**April 27, 2019**
For the baseline demo, we hooked our mbed up to a solenoid to allow us to actuate it through software---we needed a power transistor circuit for this, but this wasn't too hard to make. Now, we used the solenoid to press the spacebar once the white light was received.

On the Windows side, we got weird results when using our own program to measure difference in time measurements between Windows and mbed. We added a timer to the C program, which would start when the white square was displayed and stop when the spacebar was detected. We found that compared to the mbed's values for the same time period, the Windows timer values were lower! This wasn't expected, because we would think that Windows would take longer (as we are trying to measure the delay added by Windows) to register the spacebar press. Instead, we found that the timing values were about 30 milliseconds less on Windows compared to the mbed. We talked with our doctor, and decided to change our measurement methodology.

Instead of using our original Windows C program, we would instead use the *Cognition* program developed in part by the lab we were working with. This software has a calibration mode which allows the reaction times to be logged, after a white light is shown on the screen. We used the same mbed setup, where we would look for a white light flash, but instead actuated the solenoid to hit the spacebar as quickly as possible. This helped mimic the "ideal human" with zero latency.

We also added a pressure sensor to the spacebar, to account for the solenoid's actuation delay. It takes some time for the end of the solenoid to hit the spacebar; adding a pressure sensor and finding the time to hit the spacebar after the light flash helped us account for this and subtract it out.
![Pressure Sensor on Laptop](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Stand_Laptop.JPG "Pressure Sensor on Laptop")

Furthermore, we made a holder for the solenoid, so we could put it at a constant height above the laptop, instead of holding it.
![Stand SolidWorks](https://raw.githubusercontent.com/adityahota/NASACalibration/master/full%20stand.PNG "Stand SolidWorks")

Finally, we put all the circuitry from last week onto a protoboard, because we were getting tired of jumpers!

![Protoboard](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Protoboard.JPG "Protoboard")

## Week 2: Milestone 2 Demo
**April 19, 2019**
For our second milestone, we incorporated part of the feedback loop for our project. Our goal was to have the computer play a sound when the spacebar press was detected (using the Windows program we developed for the milestome demo); this sound would be detected as a rising edge by the mbed, stoping its timer. This would allow us to measure the time between the initial square being printed and the spacebar being pressed, to an extent.

On the Windows side, we added a command to play the beep noise---we chose to use the `beep()` function in `Windows.h`, to allow for OS-level sound generation, instead of having to rely on another program, mathematical calculations, or an external file to generate a noise. These other options could have introduced delays in our timing detection, which could throw off our results.

On the mbed side, we made circuitry to take noise from the laptop, amplify it (with an op-amp), and feed it into an input pin. We then could take this amplified noise as a rising edge and figure out when the computer recevied the spacebar press. Here is a picture of our (rather messy) circuit:
![Sound Circuit](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Sound_Circuit.JPG "Sound Circuit")

## Week 1: Milestone 1 Demo
**April 12, 2019**
Working up to the first milestone demo, we developed our first ideas of how to approach the problem of laptop timing calibration. We envisioned a system where we would have a Windows program that runs in Command Prompt and displays a white square. We would have a light sensor attached to the screen, so when the Windows program was run, the change in light would be detected by the mbed. Windows would start its timer when the square was displayed and the mbed would start its timer when the light was received.

Our first step towards this was enabling us to look for a fall edge on the mbed. We created a voltage divider using a photoresistor, where the output voltage would drop when light was detected. Then, we setup an mbed timer which would start when the falling edge was detected and fire an interrupt. For the milestone demo, our goal was to essentially figure out how to setup the timer, detect the falling edge, and fire an interrupt. The biggest challenge was getting familiar with bare metal programming on mbed, which we used in lieu of the mbed OS function calls to reduce overhead and timing delays.

For the milestone, we also created the Windows C program which would display the square. A screenshot of the C program is shown below:
![Windows C Program](https://raw.githubusercontent.com/adityahota/NASACalibration/master/Windows_Program.PNG "Windows C Program")
