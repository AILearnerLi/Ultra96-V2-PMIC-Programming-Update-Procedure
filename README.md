# Ultra96-V2-PMIC-Programming-Update-Procedure

This document is from Xilinx summer school 2020.

This document outlines the procedure for updating the programming file for the Ultra96-V2. You will need the Ultra96-V2, an Infineon programming dongle (PN USB005) and the Infineon PowIRCenter GUI software. 

https://www.infineon.com/cms/en/product/promopages/power-center-software/

You will also need the USB to PMBus header. The part number for the dongle is Infineon USB005: https://www.infineon.com/cms/en/product/power/dc-dc-converter/digital-dc-dc-multiphase-controller/usb005/

The new configuration file is available through your local FAE. You may request the file from the following web portal – Avnet.me/AvnetProgrammingFiles


The Ultra96-V2 board will need to have the 3 pin header installed on the board as shown in the image below. Samtec has these headers available here - https://www.samtec.com/products/tsw

![image](https://github.com/AILearnerLi/Ultra96-V2-PMIC-Programming-Update-Procedure/blob/master/1.png) 









The holes for the header are labeled SCL SDA and GND. GND is the pin closest to the DC power barrel jack. Connect power to the board and connect the Infineon dongle as shown, with the black wire connected to GND. 

At this stage you should be able to open up the PowIRCenter GUI, click the autopopulate button shown and see the screen below.
 
At this point you need to press the power button on the Ultra96-V2
 
After turning on the power, press the autopopulate button in the GUI again and you should see all three devices show up as is shown below. Press the circled “clear faults” button to remove false warnings that occur at startup so that all outputs are “green”  
 
At this point you are ready to load the new configuration files. First click on device x14 from the device tree, then click on the Design Wizard tab

 
Then click on load config file and select the new configuration file that corresponds to the device you wish to program. In our case since we are looking at device x14, select the file 0x14_Oct_30.txt
 

Force a write all reg command by clicking Write All Reg. 
 
Click on output D and scroll down on the commands list to IOUT_OC_FAULT_LIMIT. The value here should be 4.00A.
 
 If it does not read 4.00A, reload the config file and again click the force write.
You are now ready to write the new configuration to device memory. Click on the Utilities tab, then click on RockyR2 Device Programmer. You should see the screen below pop up.
 
Check the box next to User, then click Check MTP Left. You will see a message saying ready for programming.
 
Now click the program button, you should see the readout below when complete. 
 
At this stage you can close this popup and move on to programming the next device. We will now repeat this process for device x13. Start by clicking on device 0x13 in the device tree and follow the same procedure as before. Be sure to select the file 0x13_Oct_30.txt for programming the 2nd device.
 
Again, after loading the file, force a Write All Reg to make sure the values get updated. Now select output D of device 0x13. We are going to check the IOUT_OC_FAULT_LIMIT to make sure the update is correct. The new value should be 5.25A

 

Now proceed with programming the device as we did with device 0x14
 

Check the box next to User, then click Check MTP Left. You will see a message saying ready for programming.
 
Now click the program button, you should see the readout below when complete. 
 

Once both of these devices have been updated with the new files, you may power cycle your boards to verify that the new configuration has been loaded and saved. Output D of device 0x14 should have an IOUT_OC_FAULT_LIMIT of 4A and device 0x13 output D should have an IOUT_OC_FAULT_LIMIT of 5.25A.
You have now completed the programming updates. 
