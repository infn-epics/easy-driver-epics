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

To compile the driver, execute the **make** command from the top folder.



To configure the IP of the connected Easy Driver, edit the **./st.cmd ** from the iocBoot/iocEasyDriverTest folder. Now it is possible to execute the **./st.cmd** script  to run the easy driver ioc.


## UNIMAG interface (`unimag.db`)

`CURRENT_SP`, `CURRENT_RB`, `VOLTAGE_RB`, `STATE_SP` and `STATE_RB` follow the layout shared by
the UNIMAG power-supply IOCs. `STATE_SP`: `OFF` and `STANDBY` switch the output off, `ON` on,
`RESET` sends a reset (and does not touch the output).

`STATE_SM` tells what the supply is doing: `0 READY`, `1 GOTOSET` (readback going to the
setpoint), `2 GOTOSTATE` (commanded state not reached yet), `6 SPNOTSET` (MINOR) and
`7 STATENOTSET` (MAJOR) when the setpoint or the state is not reached within `SET_TIMEOUT_S`.
The supply is naturally bipolar: `3 GOZERO`, `4 GOPOS` and `5 GONEG` are not used. Commands are
not sent again (no `RETRY`). `SPNOTSET` / `STATENOTSET` clear when the target is reached, on a
new command, or with `STATE_SP` = `RESET`.

| PV | Description | Default |
|----|-------------|---------|
| `SET_TOLERANCE` | Readback within this of the setpoint counts as reached (A, 0 disables the setpoint check) | 0.1 |
| `SET_TIMEOUT_S` | Setpoint / state timeout, restarts on progress and on a new command (s) | 30 |

Both checks are armed by the first command after boot, so a supply left running is not reported.
