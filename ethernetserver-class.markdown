[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

# ���������� Ethernet

[\[���������� Ethernet\]](/ethernet-library.markdown)

## ����� EthernetServer

����� _EthernetServer_ ������ ������� ��� ���������� ������������ �������� �������.
���� ����� ��������� �� ������ _Server_ � ��������� ����� ������ ��� begin(), write()
� available(). ���������� �� ���������.

### ����������� EthernetServer()

����������� ���������� ������ _EthernetServer_ ����������� � ������������ ����������:

``` arduino
	EthernetServer(uint16_t port);
```

�� ���� ������������ ������� ����� ��������������� ����� _port_, ������� �������� �����
16-��������� ����������� ���������.

### ����� begin()

...

### ����� available()

...

### ����� write()

...

### ����� print()

...

### ����� println()

...

### ������

���� ������� ������ ����������� �������, ������� ������� ���� 23 (telnet), ������, ��� ���
������� ������ � ���������� ��� ��� �������.

``` arduino
	#include <SPI.h>
	#include <Ethernet.h>

	byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
	byte ip[] = { 192, 168, 1, 10 };

	EthernetServer server = EthernetServer(23);

	void setup() {
  		Ethernet.begin(mac, ip);
  		server.begin();
	}

	void loop() {
  		EthernetClient client = server.available();
  		if (client == true) {
    		server.write(client.read());
  		}
	}
```

---

[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

(c) 2015, ��������� ������� �. <easimonenko@mail.ru>
