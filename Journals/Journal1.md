# Multiple Input Case Fan Control

#### Sean Minami - 03/14/2025

Recently I have been using [FanControl](https://github.com/Rem0o/FanControl.Releases) to optimize cooling and fan noise levels in my PC.  Typically, cooling fans are controlled by a single temperature source, such as the CPU temperature sensor for the CPU cooler fans, and the GPU temperature sensor for the GPU fans.  However, users typically have to decide whether to prioritize CPU or GPU cooling when deciding which temperature sensor to use to control the case fans.

FanControl makes good use of the **Visibility of system status** usability guideline to inform users users of the current temperature of all monitored components and the speed of all fans in the system.  The figure below shows all of the parameters I am currently monitoring as well as the fan curves controlled by those parameters.  Users can clearly see the temperature of each monitored component in the system, and see how it correlates to the speed of each set of fans.  Changes to fan curve configurations are reflected by the line graph associated with that curve, and are indirectly reflected by the resulting component temperatures and fan speeds.

![FanControl Homepage](/Images/FanControlDash.png)

FanControl also utilizes the **Flexibility and Efficiency of Use** guideline to cater to users with a wide range of skill levels.  First time users are asked if they would like assistance with detecting fans and temperature sensors, then once setup is complete, there is an option to apply automatic fan curves with the user defining the temperature that the fan should try to keep the sensor at.  More advanced users can define their fan curves themselves, along with enabling hysterisis for temperature sensors, custom fan start and stop percentages, and fan ramp speeds.  Advanced users can also use the "Mix" feature to make a fan curve that depends on more than one temperature sensor.

![FanControl Assisted Setup](/Images/FanControlSetupAssist.png)

The reason I tried this piece of software was to ensure all of my case fans are spinning up when either the CPU or the GPU are getting hot.  By default, the case fans can only be controlled through the BIOS, and each fan can only be controlled by either the GPU temperature or the CPU temperature, therefore I would need to pick which component to prioritize.  This is not an ideal solution for me, since I like to play video games, which stresses the GPU, and I edit wedding videos on the side, which mostly stresses the CPU.  Depending on which component I prioritize, one of these scenarios will leave the other component with insufficient airflow to keep it cool.

The first thing I did was to press the "Plus" button to create a fan curve for the CPU and GPU, so I can define at what temperature max fan speed will be reached for each component.

![FanControl CPU Curve](/Images/FanControlCPU.png)

The second thing I did was to use the "Plus" button to add a "Mix" feature to create a fan curve that would take the average of the two previously defined curves.

![FanControl Mix](/Images/FanControlMix.png)

This achieved my initial goal of case fans being controlled by two temperature sensors, but I noticed that if one component was doing nothing, the other could be running at max temperature, and the case fans would only be running at 50%.  To fix this, I pressed the "Plus" button again to add another "Mix", and I defined this mix to take the maximum fan speed between the CPU and GPU curves, then I added this curve to the previous average function, so that the case fan speed is the average between the CPU temp, the GPU temp, and the max between CPU and GPU temp.  After doing this, the case fan speed is biased towards the hotter component.

![FanControl Mix V2](/Images/FanControlMixV2.png)

I then kept the FanControl window open while I ran through a few different use cases, and tweaked the fan curves until the noise levels and component temperatures were at a good balance.  One downside of these custom curves is that a curve or a "Mix" can both be input parameters for a "Mix", so a "Mix" with multiple curves and "Mixes" as parameters can get confusing to read.  An example is shown above, where "CPU Curve", "GPU Case Curve" and "CPU/GPU Max" all contribute to "Case Curve - Default".  This downside could become more pronounced as more "Mixes" and curves are defined.  This can also be seen as a downside for the **Visibility of System Status** usability guideline.