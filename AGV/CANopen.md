 
# CANopen Object Dictionary 
Multi-byte parameters are based on little endian(LSB first).
	*Little endian* (LSB first)
	| Bit7 | Bit6 |Bit5 |Bit4 |Bit3 |Bit2 |Bit1 |Bit0 |
	
| Index | Object  |             
| ----------- | ------------ |
| 0000        | not used    |   
| 0001 - 001F | Static Data Types (standard data types, e.g. Boolean, Integer16) |                                                
| 0020 - 003F | Complex Data Types (predefined structures composed of standard data types, e.g. PDOCommPar,     SDOParameter)     |                
| 0040 - 005F | Manufacturer Specific Complex Data Types                                                                               |
| 0060 - 007F | Device Profile Specific Static Data Types                                                                               |
| 0080 - 009F | Device Profile Specific Complex Data Types                                                                              |
| 00A0 - 0FFF | reserved                                                                                                                |
| 1000 - 1FFF | Communication Profile Area (e.g. Device Type, Error Register, Number of PDOs supported)                                   |
| 2000 - 5FFF | Manufacturer Specific Profile Area |                                                                                                                                                |
| 6000 - 9FFF | Standardised Device Profile Area (e.g. "DSP-401 Device Profile for I/0 Modules" [3]: Read State 8 Input Lines, etc.)                                                  |
| A000 - FFFF | reserved                                                                                                                                                                        |
[CANOpen Object Dictionary|500](https://www.typhoon-hil.com/documentation/typhoon-hil-software-manual/Images/canopen_slave_08.PNG)
# CANopen frame
![The CANopen frame](https://canlogger1000.csselectronics.com/img/intel/canopen/CANopen-COB-ID-Message-Format-CAN-Frame_2.png)
## Pre-Operational state(COB-id)
The 11-bit CAN ID is referred to as the **COB-ID** and is split in two parts:  
	the first 4 bits equal a **function code**,  
	the next 7 bits contain the **node ID**. Refers to 1-127 nodes (zero not allowwd)
![|500](https://canlogger1000.csselectronics.com/img/intel/canopen/CANopen-Identifier-Allocation-PDO-SDO-Standardized-Table_3.png)
### example
| COB-ID$_{hex}$ | function code$_{10-7}$ | node id$_{6-0}$ | Func  | Node ID  |
| ----------- | ------------ | ------------ | ----- | --- |
| 0x1ff       | bx0011       | bx1111111      | TPDO1 | 127 |

## CANOpen Communication interface
### [SDO (Service Data Object) protocol, page 11](https://www.nikhef.nl/pub/departments/ct/po/doc/CANopen30.pdf)
	Mailbox-like

The **SDO service** allows a CANopen node to read/edit values of another node's object dictionary over the CAN network.

SDO request and reply message always contain 8 bytes.
**Expedited transfer**: used for data objects up to 4 bytes in length.
**Segmented transfer**: for objects with length > 4 bytes.
The SDO Command Specifier contains the following information: 
♦ download(writing OD) / upload(reading OD) 
♦ request / response 
♦ segmented / expedited transfer 
♦ number of data bytes in this CAN-frame 
♦ alternating toggle bit for each subsequent segment

| Func          | SDO Command Specifier(Byte 0) | Object Index(Byte 1-2) | Object Subindex(Byte 3) |
| ---------------------- | ----------------------------- | ---------------------- | ----------------------- |
| Receive SDO(0x580+node id) | Initiate domain download      | writing 2                       |                         |
|Transmit SDO(0x600+node id )| Initiate Domain Upload        |  reading 4                      |                         |
              |                 |Download Domain Segment        |     writing 2                  |                         |
              |                 |Upload Domain Segment          |reading 4                       |                         |
              |                 |Abort Domain Transfer          |                        |                         |
### [PDO (Process Data Object) protocol, page 8](https://www.nikhef.nl/pub/departments/ct/po/doc/CANopen30.pdf)
	i/o cyclic-like
The CANopen **PDO service** is used for effectively sharing real-time operational data across CANopen nodes.
Data transfer is limited to 1 to 8 bytes (for example: one PDO can transfer at maximum 64 digital I/O values, or 4 16-bit analogue inputs).

RPDO(writing) mapping ( one cmd example )
| func                       | d_arr                   | type |
| -------------------------- | ----------------------- | ---- |
| off pdo1 cob-id             | 23 00 14 01 01 02 00 80 | u32  |
| set pdo transmit async     | 2F 00 14 02 ff - - -    | u8   |
| number of mapped object =0 | 2F 00 16 00 00 - - -    | u8   |
| pdo mapping                | 23 00 16 01 20 00 FF 60 | u32  |
| number of mapped object =1 | 2F 00 16 00 01 - - -    | u8   |
| set pdo cob-id             | 23 00 14 01 01 02 00 00 | u32  |
u16 == 2b

| send pdo cob-id  | hex      |      
| --------------- | -------- | 
| identifier      | 23       |
| function code   | 1400     | 
| sub index       | 01       |
| off/on pdo     | 80000201/00000201|

| pdo mapping     | hex           |
| --------------- | ------------- |
| identifier      | 23            |
| function code   | 1600          |
| sub index       | 01            |
| no. of bit      | 20$_h$/32$_d$ |
| subindex of obj | 00            |
| index of obj    | 60ff          |

To activate, cob-id 201, d_arr(32int) = i.e.,[00 00 14 00] velocity of 0x60ff

TPDO(reading)
### [NMT (Network Management) protocol](https://www.typhoon-hil.com/documentation/typhoon-hil-software-manual/References/canopen_protocol.html#canopen_protocol.dita__section_yc4_yjt_g3b)
Master-slave concept
### [Special function protocols](https://www.typhoon-hil.com/documentation/typhoon-hil-software-manual/References/canopen_protocol.html#canopen_protocol.dita__section_yt3_zjt_g3b)
### [Error control protocol, page 14](https://www.nikhef.nl/pub/departments/ct/po/doc/CANopen30.pdf)

- SDO is used for (large,) low-priority data transfer between devices, typically used for configuring the devices on a CANopen network. 
- PDO is used for fast data transfer of 8 bytes of data or less without protocol overhead (the meaning of the data content has been defined beforehand).
# Links
[CANopen Explained - A Simple Intro (2020)](https://youtu.be/DlbkWryzJqg)
[CANOpen protocol](https://www.typhoon-hil.com/documentation/typhoon-hil-software-manual/References/canopen_protocol.html#canopen_protocol.dita__section_whw_wht_g3b)
[COB-ID的简单理解分析](https://blog.csdn.net/jiesunliu3215/article/details/108446470)
[CANopen high-level protocol for CAN-bus](https://www.nikhef.nl/pub/departments/ct/po/doc/CANopen30.pdf)
#protocol #CAN