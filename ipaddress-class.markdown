[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

# ���������� Ethernet

[\[���������� Ethernet\]](/ethernet-library.markdown)

## ����� IPAddress

����� _IPAddress_ ������������� ������ ��� IP-�������.

### �����������

���� ���������� Ethernet ����������, �� ��� ������������� IPAddress ������ ������ ����������
�� �����. � ��������� ������ ����������� ���:

``` arduino
	#include "IPAddress.h"
```

### ����������� IPAddress()

����������� IPAddress() ���������� � ���������� ������:

``` arduino
	IPAddress()
	IPAddress(uint8\_t first\_octet, uint8\_t second\_octet, uint8\_t third\_octet, uint8\_t fourth\_octet)
	IPAddress(uint32_t address)
	IPAddress(const uint8_t *address)
```

���������� ������ �����������.

����������� _IPAddress()_ �������������� IP-����� ������� ��������� (����� 0.0.0.0).

����������� _IPAddress(uint8\_t first\_octet, uint8\_t second\_octet, uint8\_t third\_octet, uint8\_t fourth\_octet)_
�������������� IP-����� ������� ���� first\_octet.second\_octet.third\_octet.fourth\_octet.
��� ���������� ������ -- ����� ����������� ����� �������� � ����.

����������� _IPAddress(uint32\_t address)_ �������� � �������� ������ 32-���������
����������� �����, ������� ����������� ���������� ������ ���������.

����������� _IPAddress(const uint8\_t *address)_ �������� �� ���� ������ �����
����������� �����. ���� ������ ������ ����� ������ ������������������ ��������.
���� �� ������� ������ ���� ����������, ���� �������� ������ � ������� ������ ���������,
�� ���������� ����� ��������� ������ ������ � ������������� ��� ���������. ���� ��������
������, �� ���������� ��������� ����� ��������� � ���������������.

### ����� printTo()

����� _printTo()_ ��������� ��������� _Printable_ � �������� ��������� �������:

``` arduino
	virtual size_t printTo(Print& p) const;
```

� �������� ���� ����� ������������ ������������� �������� _print()_ � _println()_ ��� 
��������� ���������� ������������� ������� (����� _Print_).

### �������� uint32\_t()

�������� _uint32\_t()_ �������� ��������� �������:

``` arduino
	operator uint32_t() const { return _address.dword; };
```

�������� _uint32\_t()_ ������ �������������� ������ �� ����� ����� ������������� � ������.

### �������� ��������� (==)

�������� ��������� (==) �������� � ���� ������:

``` arduino
	bool operator==(const IPAddress& addr) const { return _address.dword == addr._address.dword; };
    bool operator==(const uint8_t* addr) const;
```

�������� ��������� ���������� ��� ������� IPAddress ��� ������ IPAdrress � IP-����� � �����
������� �� ������ �����.

### �������� ������������ (=)

�������� ������������ (=) ����������� � ���� ������:

``` arduino
	IPAddress& operator=(const uint8_t *address);
    IPAddress& operator=(uint32_t address);
```

��������� ���� ���� ����������, �� ����� �������� IP-����� � ����� ������� �� ������
����� ��� � ����� ������ ��������� �����.

### �������� ���������� ([])

�������� ���������� ��������� ���������� � ������ �� ������ ��������� IP-������
�� �����������.

```arduino
	uint8_t operator[](int index) const { return _address.bytes[index]; };
    uint8_t& operator[](int index) { return _address.bytes[index]; };
```

### ������

��������� ������ ����:

``` arduino
	#include <SPI.h>
	#include <Ethernet.h>

	byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };

	IPAddress dnServer(192, 168, 0, 1);
	IPAddress gateway(192, 168, 0, 1);
	IPAddress subnet(255, 255, 255, 0);
	IPAddress ip(192, 168, 0, 2);

	void setup() {
		Serial.begin(9600);

	  	Ethernet.begin(mac, ip, dnServer, gateway, subnet);
	  	Serial.print("IP = ");
	  	Serial.println(ip);
	}

	void loop() {
	}
```

### ����������

������ IPAddress ����� �������� � ����

``` arduino
	union {
		uint8_t bytes[4];
		uint32_t dword;
    } _address;
```

����� �������, ��� ����� ������������� ������ ������������ � ����� ��������������
����� �����.

---

[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

(c) 2015, ��������� ������� �. <easimonenko@mail.ru>
