[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

# Библиотека Ethernet

[\[Библиотека Ethernet\]](/ethernet-library.markdown)

## Объект Ethernet

Объект _Ethernet_ инициализирует библиотеку Ethernet и позволяет задать сетевые настройки.
Является экземпляром класса _EthernetClass_.

### Ethernet.begin()

Метод _Ethernet.begin()_ производит инициализацию библиотеки и позволяет задать сетевые
настройки. Вызов метода возможен в одной из нескольких следующих форм:

``` arduino
	Ethernet.begin(mac);
	Ethernet.begin(mac, ip);
	Ethernet.begin(mac, ip, dns);
	Ethernet.begin(mac, ip, dns, gateway);
	Ethernet.begin(mac, ip, dns, gateway, subnet); 
```

Библиотека Ethernet поддерживает _DHCP_. Для автоматического получения IP-адреса метод
нужно вызывать в форме `Ethernet.begin(mac);`. В этом случае метод возвращает успех
(число 1), если адрес по DHCP получен, и число 0 -- в противном случае. В остальных
вариантах вызова метод ничего не возвращает.

Первый параметр, mac, должен быть массивом из шести беззнаковых байт. Остальные
параметры являются объектами класса IPAddress. Допускается передавать вместо
экземпляра IPAddress значения, из которых он может быть сконструирован. IPAddress
рассматривается ниже.

Рассмотрим назначение этих параметров.

- _mac_: MAC-адрес Ethernet Shield.

- _ip_: IP-адрес Ethernet Sheild.

- _dns_: IP-адрес DNS-сервера; если не задан, то IP-адрес содержит в последнем октете 1.

- _gateway_: IP-адрес шлюза; если не задан, то IP-адрес содержит в последнем октете 1.

- _subnet_: маска подсети; по умолчанию это 255.255.255.0.

Небольшой пример кода с методом Ethernet.begin():

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

Метод _Ethernet.localIP()_ позволяет узнать IP-адрес Ethernet Shield. Используется,
когда IP-адрес был назначен DHCP-сервером. Метод не получает никаких параметров и
возвращает объект класса _IPAddress_.

### Ethernet.dnsServerIP()

Метод _Ethernet.dnsServerIP()_ возвращает IP-адрес DNS-сервера. Метод не получает никаких
параметров и возвращает объект класса _IPAddress_.

### Ethernet.gatewayIP()

Метод _Ethernet.gatewayIP()_ возвращает IP-адрес шлюза. Метод не получает никаких
параметров и возвращает объект класса _IPAddress_.

### Ethernet.dnsServerIP()

Метод _Ethernet.dnsServerIP()_ возвращает IP-адрес DNS-сервера. Метод не получает никаких
параметров и возвращает объект класса _IPAddress_.

### Ethernet.subnetMask()

Метода _Ethernet.subnetMask()_ возвращает маску подсети. Метод не получает никаких
параметров и возвращает объект класса _IPAddress_.

### Ethernet.maintain()

Метод _Ethernet.maintain()_ позволяет перепривязать или обновить выданный DHCP-сервером адрес.
Метод не получает никаких параметров и возвращает одно из следующих значений типа int:

* 0: ничего не получено;

* 1: обновление неуспешно;

* 2: обновление успешно;

* 3: перепривязка неуспешна;

* 4: перепривязка успешна.

### Пример

Небольшой пример кода с методами объекта Ethernet:

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

### Примечание

Судя по коду библиотеки Ethernet на момент написания этой главы, класс EthernetClass
почти класс-одиночка (Singleton). Почти в том смысле, что код класса не является
кодом одиночки, но в целом класс ведёт себя как одиночка. Создавать ещё один экземпляр
EthernetClass нет смысла, тем более, что установка ещё одного Ethernet Shield не
предусмотрена (на шилде нет колодки ICSP/SPI), а код низкого уровня рассчитан только на
работу с одним чипом WIZnet W5100.

---

[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
