Int to byte method
```cpp
void int_to_byte(int32_t acc) {
	std::vector<BYTE> byte = { 0x00, 0x88, 0x00, 0x00, 0x00, 0x00 };

	byte[2] = (acc >> 24) & 0xff;
	byte[3] = (acc >> 16) & 0xff;
	byte[4] = (acc >> 8) & 0xff;
	byte[5] = (acc >> 0) & 0xff;


	for (int i = 0; i < 6; i++) {
		printf("%02X\n", byte[i]);
	}

	return true;
};
```
