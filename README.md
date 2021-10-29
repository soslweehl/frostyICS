# frostyICS &#127981;
Industrial control system cyber range with objective to disrupt heating system.

# TL;DR

This is a cyber range containing two physical systems (Heating plant and warehouse management system). Heat plant controls heat supply to the city districts, and warehouse management system controls warehouse lights and alarms. This cyber range consists of 4 main components 2 SCADAs and 2 PLCs. Mainly Siemens products are used in this project.

# Topology

Cyber range network topology is shown below. The system consists of two PLCs, SCADA and WEB-SCADA. So  CR can be divided into control and execution sections. The Control section contains SCADA, and execution contains PLCs. For PLC S7-1200 in CR, hardware-in-the-loop (HIL) is used to simulate the heating process. HIL consists of a simplified mathematical model of the physical healing process. HIL includes and controls nominal values of the physical process to be damaged if nominal values are exceeded. For PLC LOGO! There is no complex physical process to simulate as the PLC LOGO! controls state of lights and alarm.

For the operator to visualize and interact with the process, SCADAS is used in this case. SCADA can also be used for the attacker to understand the state and purpose of the system. The heating process is visualized using WinCC SCADA. WinCC is the run-time of the SCADA program and can be created in the TIA portal. WinCC is computer software hence can be run in Windows virtualized environment, making it easier to reproduce and expand. Windows can also increase the attack surface of the CR. Also, SCADA and engineering software for most of the vendors can be downloaded and used for the trial period, which is a financially favorable solution.

The SCADA and PLC S7-1200 were configured and programmed utilizing Siemens software TIA Portal. The TIA Portal is a multipurpose platform that allows the program PLCs and other peripheral devices like networking elements, HMI's, SCADA. TIA Portal allows fully functional simulation and emulation of the programmed environment. TIA Portal allows access to the devices online. It also allows the user to access the diagnostics functionality embedded in the devices in real-time.

![image-20210527201603455](./docs/img/image-20210527201603455.png)



# Working principle

## Heating system

Logic and Heating process simulation is on S7-1200 PLC and visualization are in SCADA.



SCADA HMI visualization of the heating plant is shown bellow. The heating plant consists of:

- Heating transmission line - transports heat transfer fluid (HTF) to the city;
- Circulation pump (A1) - forces the HTF flow to the city;
- Transmission line valve (A3) - required to be open for the HTF to circulate;
- Gas flow valve (A2) - control the burning temperature of the gas in the burning chamber;
- Temperature and pressure sensors (S3, S4) - to monitor and give feedback to the control system about temperature and pressure in HTF tank;
- Flow speed sensor (S1) - To monitor and give feedback to the control system about the state of the HTF flow speed.
- 

The heating process can be divided into two phases. One of the phases is the heating of HTF, and the second is HTF transmission to the city districts:


- HTF is heated by burning gas in the furnace. Then the heated fluid is distributed to the rural area. Gas flow is related to the burning temperature. Burning temperature is controlled by gas flow valve A2. To automate the burning process, an operator sets a setpoint with the desired fluid temperature level. S7-1200 PLC compares setpoint temperature with the actual heat transfer fluid temperature S4. Based on that, S7-1200 PLC controls gas-burning temperature S2  by adjusting gas flow controller A2. This system has embedded physical limits, such as, maximum temperature and maximum pressure. After exceeding maximum values, the heating plant gets damaged. If temperature or pressure values reach a set threshold, S7-1200 automation protects  the physical system by stopping the gas flow to safeguard against the damage;
	
- The HTF transmission process depends on the heating process. When HTF in the transmission line reaches temperature 60° C, then circulation pump A1 switches on, and heating valve A3 opens. In this phase heating system is fully operational, and heat is delivered to the city districts. However, this part of the system can be damaged irreversibly if the circulation pump runs with the heating liquid valve (A3) closed.




![image-20210527202214373](./docs/img/image-20210527202214373.png)



## Warehouse management system

Logic of warehouse management runs on LOGO! and visualization resides on WEB-SCADA

Warehouse management in this CR is used to control alarms and lights. This process is much simpler than the heating plant. Siemens LOGO! 8.2 PLC is used to control it as it is meant for simple applications. LOGO! can have different configurations depending on added functional modules. In this CR LOGO! 8.2 basic module is used with built-in I/O and communication interface.

![image-20210527202345694](./docs/img/image-20210527202345694.png)



# Requirements

Following are hardware and software required to set up the lab. Additionally alternatives for each device are briefly described. To check device parameters and search for MLFB codes Siemens SIOS website can be used https://support.industry.siemens.com/ .

<table>
<thead>
  <tr>
    <th>Nr.</th>
    <th>Element</th>
    <th>System description</th>
    <th>MLFB order code</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3">1</td>
    <td rowspan="3">SCADA</td>
    <td>Siemens, SIMATIC WinCC Advanced&nbsp;&nbsp;&nbsp;V15.1</td>
    <td>6AV2102-0AA05-0AA5 </td>
  </tr>
  <tr>
    <td>Windows&nbsp;&nbsp;&nbsp;7 enterprise, SP1, Build 7601</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>VirtualBox&nbsp;&nbsp;&nbsp;V6.0</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td rowspan="3">2</td>
    <td rowspan="3">WEB-SCADA</td>
    <td>NodeRed V1.0.0</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>Yocta&nbsp;&nbsp;&nbsp;Linux V2.6</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>IOT2040</td>
    <td>6ES7647-0AA00-1YA2</td>
  </tr>
  <tr>
    <td>2</td>
    <td>PLC LOGO!</td>
    <td>Siemens, LOGO! 8.2, Full&nbsp;&nbsp;&nbsp;versions: 1.82.02</td>
    <td>6ED1052-1FB08-0BA0</td>
  </tr>
  <tr>
    <td>3</td>
    <td>PLC s7-1200</td>
    <td>Siemens, SIMATIC S7-1200, CPU&nbsp;&nbsp;&nbsp;1215C</td>
    <td>6ES7215-1AG40-0XB0</td>
  </tr>
</tbody>
</table>

Additional information about used software in in the project:

| Software                 | Description                                                  |
| ------------------------ | ------------------------------------------------------------ |
| TIA portal V15 or higher | For trial period can be downloaded from here https://support.industry.siemens.com/cs/document/109761045/simatic-step-7-and-wincc-v15-1-trial-download . This is link for 15.1 version, project version should match with TIAportal version. It is important to note that to get this trial can take up to several day as registration to Siemens site takes some time |
| LOGO! Softcomfort        | LOGO! soft comfort has trial, however it doesn't has capability to upload project to PLC https://new.siemens.com/global/en/products/automation/systems/industrial/plc/logo/logo-software.html#Demosoftware. Full version can be bought. Unfortunately currently software can be bought in CD and cant be downloaded. You should consult with Siemens representatives in your country. This software is relatively cheep, you could cut on some bears and you will have this software :) |
| NodeRed                  | https://nodered.org/                                         |
| Windows 7 or higher      | Can be run in virtual machine. I suggest using two different WIN machines, one as SCADA machine for actual network and second as engineering station. Both will contain TIAportal and heating [project](https://github.com/austrisu/frostyICS/tree/main/config_files/S7-1200%20and%20wincc), but it will be simpler to deploy everything. |

# Installation instructions

- TiaPortal v15 and v16 project upload to the S7-1200   [s71200-project-upload.md](docs/s71200-project-upload.md) 
- LOGO! Soft Comfort installation and project upload is described here [logo-project-upload.md](docs/logo-project-upload.md)

## Test excersise scenario

FrostyICS was used to perform training. Information about test scenario and execution principles can be found in:

-   [excersise-scenario.md](docs/test-excersise/excersise-scenario.md) 
- Anonymized link

# Resources

TIAportal and WinCC (S7-1200 and SCADA)

- TIAportal trial download - https://support.industry.siemens.com/cs/document/109761045/simatic-step-7-and-wincc-v15-1-trial-download 
- TIAportal usage are described here  - https://www.youtube.com/watch?v=GgKMGj0aXQw
- Getting and isntalling TIA  Portal V15 and V16 - https://www.youtube.com/watch?v=xE25v2Y2_t4&list=PLtGimRyb0S0ivKG6RsDWTtPSyOZ_iqS3b
- TIA  Portal Hardware configuration - https://www.youtube.com/watch?v=lqHIKYUWXvs&list=PLtGimRyb0S0ivKG6RsDWTtPSyOZ_iqS3b&index=2
- TIA Portal HMI programming - https://www.youtube.com/watch?v=cUN7lic-1hE&list=PLtGimRyb0S0hgH5mWFTIo1DkP0kiG-qhU
- TIA Portal programming full course - https://www.youtube.com/channel/UC1P4ACs0hsr7AWcl-mWKQbQ/playlists

LOGO!

- LOGO! SoftComfort usage are best explained here - https://www.youtube.com/watch?v=xbK3ngp70hM&list=PLRtRKudOMmtFVIVcH0AMX4h9rszwDPXEE

Additional

- Search for different Siemens related questions about hardware and software - https://support.industry.siemens.com
- Additional information about creation of this cyber range - anonymized link



