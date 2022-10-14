# Introduction
+ Modbus ASCII
+ Modbus RTU
+ Modbus TCP
# Modbus RTU
Transmit: Serial
Decode: 8-bits
Check digit: CRC16

|Address|Function|Data                                      |CRC  |
|---------|-----‐---|-----‐-------------------------|-----‐-|
|8bits     |8bits      |nx8bits(n- length of fuction)|16bits|

*(1 byte = 8bits = 2hex digits)*


## crc python code
```py
    def calc_crc16(self, data):
    """
    return crc values of modbus rtu
    """   
    crc = 0xFFFF    
	for pos in data:
		crc ^= pos
		for i in range(8):
			if((crc & 1) != 0):
				crc >>= 1
				crc ^= 0xA001
			else:
				crc >>= 1
	print(hex((crc & 0xff)), hex(crc >> 8))
	return [(crc & 0xff) , (crc >> 8)]

```
## Example
Field name   hex
------------------------------
Slave Address           11 
Function                    01 
Starting Address Hi   00 
Starting Address Lo  13 
No. of Registers Hi    00 
No. of Registers Lo   03
Error Check               crc16



# Links
[Modbus RTU 通訊協定介紹](http://www.vx-hmi.com/doc/Modbus%20RTU%20%E7%B0%A1%E4%BB%8B.pdf)
[Modicon Modbus Protocol Reference Guide](https://modbus.org/docs/PI_MBUS_300.pdf)

#protocol