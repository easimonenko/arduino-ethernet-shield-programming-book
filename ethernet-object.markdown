[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

# ���������� Ethernet

[\[���������� Ethernet\]](/ethernet-library.markdown)

## ������ Ethernet

������ _Ethernet_ �������������� ���������� Ethernet � ��������� ������ ������� ���������.
�������� ����������� ������ _EthernetClass_.

### Ethernet.begin()

����� _Ethernet.begin()_ ���������� ������������� ���������� � ��������� ������ �������
���������. ����� ������ �������� � ����� �� ���������� ��������� ����:

``` arduino
	Ethernet.begin(mac);
	Ethernet.begin(mac, ip);
	Ethernet.begin(mac, ip, dns);
	Ethernet.begin(mac, ip, dns, gateway);
	Ethernet.begin(mac, ip, dns, gateway, subnet); 
```

���������� Ethernet ������������ _DHCP_. ��� ��������������� ��������� IP-������ �����
����� �������� � ����� `Ethernet.begin(mac);`. � ���� ������ ����� ���������� �����
(����� 1), ���� ����� �� DHCP �������, � ����� 0 -- � ��������� ������. � ���������
��������� ������ ����� ������ �� ����������.

������ ��������, mac, ������ ���� �������� �� ����� ����������� ����. ���������
��������� �������� ��������� ������ IPAddress. ����������� ���������� ������
���������� IPAddress ��������, �� ������� �� ����� ���� ��������������. IPAddress
��������������� ����.

���������� ���������� ���� ����������.

- _mac_: MAC-����� Ethernet Shield.

- _ip_: IP-����� Ethernet Sheild.

- _dns_: IP-����� DNS-�������; ���� �� �����, �� IP-����� �������� � ��������� ������ 1.

- _gateway_: IP-����� �����; ���� �� �����, �� IP-����� �������� � ��������� ������ 1.

- _subnet_: ����� �������; �� ��������� ��� 255.255.255.0.

��������� ������ ���� � ������� Ethernet.begin():

``` arduino
	#include <SPI.h>
	#include <Ethernet.h>

	byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
	byte ip[] = { 192, 168, 1, 1 };

	void setup() {
  		Ethernet.begin(mac, ip);
	}

	void loop () {
	}
```

### Ethernet.localIP()

����� _Ethernet.localIP()_ ��������� ������ IP-����� Ethernet Shield. ������������,
����� IP-����� ��� �������� DHCP-��������. ����� �� �������� ������� ���������� �
���������� ������ ������ _IPAddress_.

### Ethernet.dnsServerIP()

����� _Ethernet.dnsServerIP()_ ���������� IP-����� DNS-�������. ����� �� �������� �������
���������� � ���������� ������ ������ _IPAddress_.

### Ethernet.gatewayIP()

����� _Ethernet.gatewayIP()_ ���������� IP-����� �����. ����� �� �������� �������
���������� � ���������� ������ ������ _IPAddress_.

### Ethernet.dnsServerIP()

����� _Ethernet.dnsServerIP()_ ���������� IP-����� DNS-�������. ����� �� �������� �������
���������� � ���������� ������ ������ _IPAddress_.

### Ethernet.subnetMask()

������ _Ethernet.subnetMask()_ ���������� ����� �������. ����� �� �������� �������
���������� � ���������� ������ ������ _IPAddress_.

### Ethernet.maintain()

����� _Ethernet.maintain()_ ��������� ������������� ��� �������� �������� DHCP-�������� �����.
����� �� �������� ������� ���������� � ���������� ���� �� ��������� �������� ���� int:

* 0: ������ �� ��������;

* 1: ���������� ���������;

* 2: ���������� �������;

* 3: ������������ ���������;

* 4: ������������ �������.

### ������

��������� ������ ���� � �������� ������� Ethernet:

``` adruino
	#include <SPI.h>
	#include <Ethernet.h>

	byte mac[] = {0x00, 0xAA, 0xBB, 0xCC, 0xDE, 0x02};

	void setup() {
  		Serial.begin(9600);
  		if (Ethernet.begin(mac) == 0) {
    		Serial.println("Failed to configure Ethernet using DHCP!");
    		while (true) {
			}
  		}
  		Serial.println(Ethernet.localIP());
		Serial.println(Ethernet.dnsServerIP());
		Serial.println(Ethernet.gatewayIP());
		Serial.println(Ethernet.dnsServerIP());
		Serial.println(Ethernet.subnetMask());
	}

	void loop() {
	}
```

### ����������

���� �� ���� ���������� Ethernet �� ������ ��������� ���� �����, ����� EthernetClass
����� �����-�������� (Singleton). ����� � ��� ������, ��� ��� ������ �� ��������
����� ��������, �� � ����� ����� ���� ���� ��� ��������. ��������� ��� ���� ���������
EthernetClass ��� ������, ��� �����, ��� ��������� ��� ������ Ethernet Shield ��
������������� (�� ����� ��� ������� ICSP/SPI), � ��� ������� ������ ��������� ������ ��
������ � ����� ����� WIZnet W5100.

---

[\[� ������\]](/readme.markdown) | [\[���������� SD\]](/sd-library.markdown)

---

(c) 2015, ��������� ������� �. <easimonenko@mail.ru>
