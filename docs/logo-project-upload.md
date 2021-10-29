# Unloading configuration to PLC (LOGO!)

This software is installed as any typical application on windows machine. Nothing specific to tell here

Following are steps on how to upland configuration to LOGO!



Download https://github.com/soslweehl/frostyICS/tree/main/config_files/logo! and open in following way

![image-20210504205144855](../docs/img/image-20210504205144855.png)


![image-20210504205242134](../docs/img/image-20210504205242134.png)



Modifying IP address of target LOGO! if it is necessary:

![image-20210504205332650](../docs/img/image-20210504205332650.png)

![image-20210504205405309](../docs/img/image-20210504205405309.png)



If IP is changed Modbus and S7 partner devices need to be updated:

![image-20210504205545428](../docs/img/image-20210504205545428.png)



S7 configuration:

![image-20210504205704942](../docs/img/image-20210504205704942.png)



Uploading project to the  PLC:

![image-20210504205823986](../docs/img/image-20210504205823986.png)



Before uploading Soft Comfort will ask to search for device and choose to which of available devices to upload the project:

![image-20210504210022963](../docs/img/image-20210504210022963.png)



When project is downloaded to device you can see LOGO parameters on LOGO display and do some simple adjustments.

To debug the program if any changes are made can be done using built in tools. Online test allows to connect to PLC and check the status of program in the PLC

![image-20210504210553460](../docs/img/image-20210504210553460.png)