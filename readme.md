# CAEN ELS Easy Driver - EPICS driver


Version 0.1.35

This software is compatible with:

- Easy Driver

The driver is inspired on the SY3634 EPICS driver (A36xx Norum driver).



## Configuration:

Modify the **configure/RELEASE** file and put the correct ASYN and EPICS_BASE paths.

The script was tested with:

- **base 3.14.12.5** and 
- **asyn 4.18**

To compile the driver, execute the **make** command from the top folder

Once the driver is correctly compiled it is possible to execute the ioc with the **./st.cmd ** from the iocBoot/iocEasyDriverTest folder.

