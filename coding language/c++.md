## Data type
| Specifier    | Common     |  Bits | Bytes | Minimum Value | Maximum Value |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------- | ---------- | ------- | ---- | ----- | ------------- | ------------- |
| int8_t  | signed char		|8	|1	|-128	|127    
| uint8_t  | unsigned char		|8|	1	|0|	255                      |               |               |
| int16_t    | short		|16|	2	|-32,768|	32,767                             |            |         |      |       |               |               |
| uint16_t   | unsigned 	|	16|	2|	0|	65,535                       |               |
| int32_t   | int		|32|	4|	-2,147,483,648	|2,147,483,647                    |            |         |      |       |               |               |
| uint32_t   | unsigned int		|32|	4|	0	|4,294,967,295                    |            |         |      |       |               |               |
| int64_t    | long long	|	64	|8	|-9,223,372,036,854,775,808|9,223,372,036,854,775,807 |            |         |      |       |               |               |
| uint64_t	|unsigned long long		|64	|8	|0|	18,446,744,073,709,551,615 |                                                                           |            |         |      |       |               |               |

————————————————

## Int to byte method
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
## pointer (ptr)
for, 
```cpp
	int arr[size];
	int \*ptr = &arr;
```
then,
```cpp
	memory address： &arr[i] == ptr+i
	values： arr[i]  == \*(ptr+i)
```

#### input:
```cpp
// C++ program to illustrate sizes of
// pointer of array
#include <bits/stdc++.h>
using namespace std;

int main()
{
	int arr[] = { 3, 5, 6, 7, 9 };
	int *p = arr;
	int (*ptr)[5] = &arr;
	
	cout << "p = "<< p <<", ptr = " << ptr << endl;
	cout << "*p = "<< *p <<", *ptr = " << *ptr << endl;
	
	cout << "sizeof(p) = "<< sizeof(p) <<
			", sizeof(*p) = " << sizeof(*p) << endl;
	cout << "sizeof(ptr) = "<< sizeof(ptr) <<
		", sizeof(*ptr) = " << sizeof(*ptr) << endl;
	return 0;
}

// This code is contributed by shubhamsingh10

```
#### output
```cpp
p = 0x7ffde1ee5010, ptr = 0x7ffde1ee5010
*p = 3, *ptr = 0x7ffde1ee5010
//p is ptr of arr[0], ptr is ptr of &arr
sizeof(p) = 8, sizeof(*p) = 4
sizeof(ptr) = 8, sizeof(*ptr) = 20
```
### ptr array
```cpp
for (int i = 0; i < 8; i++) { 
		printf("memory: %02x \t", &_read_tq_tx[i]);
		printf("values: %02x ", _read_tq_tx[i]);
		std::cout  << std::endl;
	}
```

# Links
[C中int8_t, int16_t, int32_t, int64_t, uint8_t, size_t, ssize_t區别](https://blog.csdn.net/yz930618/article/details/84785970)
[Pointer to an Array | Array Pointer](https://www.geeksforgeeks.org/pointer-array-array-pointer/)