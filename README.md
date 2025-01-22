# WHAT IS THIS?
This is a custom fork of [LibreHardwareMonitor](https://github.com/LibreHardwareMonitor/LibreHardwareMonitor) to expand compatibility to new AM5 and LGA1851 motherboards (Primarily MSI Boards) using the Nuvoton NCT6687D Super I/O Controller, with a specific focus on fixing [FanControl](https://github.com/Rem0o/FanControl.Releases) functionality.

## LibreHardwareMonitor
If you're here, then you already know what LHM is. 

## Motherboard Compatibility Chart
| Manufacturer | Model | Fan Controlability | Correct Voltage Sensor Readout | Correct Temperature Sensor Layout | Community Vetted |
| -------- | ------- | -------- | ------- | -------- | ------- |
| MSI | MAG X870 TOMAHAWK WIFI | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| MSI | PRO X870-P WIFI | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| MSI | MPG X870E CARBON WIFI | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| MSI | MAG X870E TOMAHAWK WIFI | :white_check_mark: | :hammer: | :white_check_mark: | :white_check_mark: |
| MSI | MAG Z890 TOMAHAWK WIFI | :grey_question: | :grey_question: | :grey_question: | :x: |
| MSI | MPG Z890 CARBON WIFI | :white_check_mark: | :hammer: | :white_check_mark: | :white_check_mark: |

**Note:** Since I do not own all of these motherboards, the compatibility is largely dependant on your cooperation. The more dialogue we have and the more motherboard data you share directly affects how quickly compatibility for your motherboard improves.

## How do I get my motherboard added?
First off, verify that your motherboard uses the Nuvoton NCT6687D Super I/O controller. If it does not, can't help ya. If it does, please open an issue containing the following information: 
 - **LibreHardwareMonitor Report** - This can be generated by going to File > Save Report in LibreHardwareMonitor. If you'd like to sensor the data within, please make sure you _only_ include data in the "Hardware Monitor Registers" section of the report. This section is terminated by a long series of hyphens.
 - **Full name of Motherboard** - LHM should identify the motherboard properly, but if not, HWMonitor might be able to. When dealing with MSI motherboards, the full name should appear similar to the following: `MAG X870 TOMAHAWK WIFI (MS-7E51)` Note the trailing model number in parenthesis. It is imperative that this information be accurate, as our current solution relies on properly identifying the motherboard. 

 **Please search for an existing open issue for your motherboard before creating a new one. Duplicate issues for the same motherboard will be closed!**

## Installation w/ FanControl

1. Exit FanControl and ensure it is no longer running on your system before continuing. 
2. Make a Backup your current FanControl directory by copying it to a safe location.
3. Ensure you have the .NET 4.8 version of FanControl (being investigated, I can't replicate issues with running other .NET versions on my end)
4. Extract the content of the Net472 folder within the downloaded .Zip to your FanControl directory and replace all files.
5. Upon launching FanControl, you'll have to create an all new configuration. Follow the wizard step-by-step to do so.
6. Manually pair the speed sensors to the detected fans. This is dude to the system fans not responding as quickly as FanControl anticipates. We're working on trying to find a solution.
7. Save the configuration. If you want to copy over your previous fan curves, etc. You can attempt to do so by opening the previous configuration JSON and copying and pasting the values to the new configuration JSON. YMMV.

## Known Issues

- System Fans do not ramp up or down as quickly as CPU Fan, instead it obeys the value set in the BIOS. It's highly recommended that you set the "Step Up" and "Step Down" times for all System Fans to "0.1 seconds" so the fans can respond as fast as possible.
- Because the System Fans do not adjust quick enough, FanControl becomes "impatient" and will not automatically pair the Fan RPM Speed Sensor with the appropriate System Fans, however, they will be labeled properly. You will have to manually pair the speed sensor to the fan controls to exert proper command over each system fan. A solution is being sought for this issue.
- Additionally, because of this behavior, you will most likely have to manually adjust parts of each fan's calibration, as FanControl will likely store (and therefore expect) the wrong RPM at the requested PWM %. To do this, manually calibrate the fan of your choice, set it to the desired speed using the slider, then wait 10-15 seconds for the fan RPM to adjust and settle. Then, using the table on the right, enter the approximate RPM value that coincides with your currently requested speed %.

## License
LibreHardwareMonitor is free and open source software licensed under MPL 2.0. You can use it in private and commercial projects. Keep in mind that you must include a copy of the license in your project.
