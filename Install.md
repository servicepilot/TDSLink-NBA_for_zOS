
# Installing ServicePilot TDSLink - NBA for z/OS

## Requirements

- z/OS v1r5 to v2r5
- A product key - *Only for the commercial version of this software*
- The software from this repository

## Installation

### 1. Download and unzip files

   1. Download [TDSLink-NBA_for_zOS.zip](TDSLink-NBA_for_zOS.zip) from this site
   
   2. Unzip TDSLink-NBA_for_zOS.zip

### 2. Upload and receive NBA for z/OS load file

   1. Upload `NBA_for_zOS_9.0_yyqqq.xmi` from the unzipped folder (previous step) with **FTP** or **IND$FILE** to z/OS using a binary file transfer method (no CRLF or ASCII translation) into a dataset (e.g.: `NBA4ZOS.TEMP.XMI`) with the following format:

          LRECL=80,RECFM=FB,DSORG=PS

   2. On **TSO**, issue the `RECEIVE` command to put the file into PDS format:

          => TSO RECEIVE INDATASET(‘NBA4ZOS.TEMP.XMI’)

      When prompted by the `RECEIVE` command, enter:

          DA(‘NBA4ZOS.V90.LOAD’) UNIT(unit) VOLUME(volume)

### 3. Perform APF authorization for NBA for z/OS LOADLIB

Use either a *Static* or *Dynamic* APF authorization.

#### Static

   1. Create or modify `PROGxx` in your **PARMLIB**
   2. Define the NBA for z/OS LOADLIB and its volume
   3. Then, activate it (`SET PROG=xx`)

#### Dynamic

   1. The command below allows a dynamic definition in console mode:

          SETPROG APF ADD DSN=NBA4ZOS.V90.LOAD,VOL=......

### 4. Create the started task – STC

   1. Create the STC into a system **PROCLIB** - e.g.: `SYS1.PROCLIB(NBA4ZOS)`
   **Example:**

          //NBA4ZOS PROC
          //*
          //NBA4ZOS EXEC PGM=PTDS,TIME=1440,REGION=0M
          //*
          //STEPLIB  DD DISP=SHR,DSN=NBA4ZOS.V90.LOAD
          //SYSIN    DD DUMMY
          //*SYSIN   DD DISP=SHR,DSN=NBA4ZOS.PARMLIB(SYSIN)
          //SYSABEND DD SYSOUT=*
          //TDSLOG   DD SYSOUT=*
          //SYSTRACE DD SYSOUT=*
          //TLOALARM DD SYSOUT=*
          //*

   2. Customize the started task.

### 5. Define RACF authorization

   1. Define NBA for z/OS to RACF and authorize NBA for z/OS userid to use Open Edition Services. If necessary, contact your security administrator.

      Below is a job with a RACF definition example:

          //RACF JOB
          //*
          //* Define RACF resources for NBA for z/OS
          //*
          //RACF EXEC PGM=IKJEFT01
          //SYSTSPRT DD SYSOUT=*
          //SYSTSIN  DD *
            AG nbagrp OWNER(racfadmuser)
            AU nbauser OWNER(racfadmuser) DFLTGRP(nbagrp) NOPASSWORD
            RDEF STARTED NBA4ZOS.* STDATA(USER(nbauser)) OWNER(racfadmuser)
            SETROPTS RACLIST(STARTED) REFRESH
            ALG nbagrp OMVS(GID(nnn))
            ALU nbauser DFLTGRP(nbagrp) NOPASSWORD OMVS(UID(nnn))
          /*

> **Note:**
>  - The `nnn` wildcard must be replaced by the Group ID and the User ID you chose.
> - The `nbagrp` and `nbauser` wildcards must be replaced by the NBA for z/OS Free Edition Group and User name you chose.
> - The `racfadmuser` wildcard must be replaced by the RACF owner user.

   2. [if required by installation]

      Authorize NBA for z/OS to access the files defined in the start procedure.

   3. [if required by installation]

      Authorize NBA for z/OS to send commands such as `V TCPIP,,PKT`.

      To do so, NBA for z/OS userid must access the MVS.VARY.TCPIP.* profile of the OPERCMDS class with the CONTROL level.

### 6. Define the NBA for z/OS parameters (in the optional SYSIN file or the STC parm)

When defining NBA for z/OS parameters, priority is given to the STC parameters (`PARM=` in the `EXEC` card).

          //NBA4ZOS  PROC
          //NBA4ZOS EXEC PGM=PTDS,PARM='WEBPORT=80',TIME=1440,REGION=0M

When a parameter is defined in the STC, it may be overridden with `PARM=` in the start command

          S NBA4ZOS,PARM='WEBPORT=8080'

If a parameter is not defined, NBA for z/OS looks in the SYSIN file and finally in the NBA for z/OS "Defaults".

   1. Upload the Sysin.txt file sample into a system **PARMLIB** - e.g.: `NBA4ZOS.PARMLIB(SYSIN)`

   2. Customize the SYSIN parameter "KEY" to define the product password for the commercial license.


> **Note:** The continuation character allows parameters to be defined on several lines. If one line ends with the ',' (comma) character then the following line will be concatenated with the current one.
>
> Example:
>
>     OUTPUT SPILOT,111.222.33.44,
>       514,Class_name,Obj_name,View_name

> **Warning:** Bad use of the continuation character may cause NBA for z/OS to ignore or misinterpret parameters.

### 6. Optional HTTPS web interface access

The TDSLink - NBA for z/OS agent includes a web interface serving pages using HTTP. To secure this interface with HTTPS it is necessary to implement **AT-TLS** technology.

See [Access ServicePilot TDSLink - NBA for z/OS using HTTPS](https.md) for details on securing the web interface.

---

## Using ServicePilot TDSLink - NBA for z/OS

### Starting TDSLink - NBA for z/OS

Use the following MVS command:

          S NBA4ZOS
 
Any SYSIN or DEFAULT parameters may be overridden with PARM=

          S NBA4ZOS,PARM='WEBPORT=8080'
 
### Stopping TDSLink - NBA for z/OS

Use the following MVS command:

          P NBA4ZOS

or the following internal command:

          Z FORCE

### Automatic start/stop

NBA for z/OS can be started and stopped automatically when TCP/IP starts and stops. The STC name must be added to the AUTOLOG statement in the hlq.PROFILE.TCPIP data set.

          AUTOLOG 5
           NBA4ZOS
          END AUTOLOG

## Support

For any question or contribution, you can contact us at: [support@servicepilot.com](mailto:support@servicepilot.com?subject=ServicePilot%20NBA%20for%20z/OS)

## Copyright

© Copyright ServicePilot Inc 2023
