[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

# Библиотека Ethernet

В этой главе делается обзор библиотеки _Ethernet_, её классов, объектов и их методов.
Примеры использования этой библиотеки рассматриваются в следующих главах.

## Подключение библиотеки

Библиотека Ethernet является стандартной и для своей работы требует также подключённую
библиотеку _SPI_. Код для подключения библиотек в скетче следующий:

``` Arduino
	#include <SPI.h>
	#include <Ethernet.h>
```

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

## Класс IPAddress

Класс _IPAddress_ предоставляет обёртку для IP-адресов.

### Подключение

Если библиотека Ethernet подключена, то для использования IPAddress ничего больше подключать
не нужно. В противном случае подключайте так:

``` arduino
	#include "IPAddress.h"
```

### Конструктор IPAddress()

Инициализирует IP-адрес нулевым значением (адрес 0.0.0.0).

### Конструктор IPAddress(uint8\_t first\_octet, uint8\_t second\_octet, uint8\_t third\_octet, uint8\_t fourth\_octet)

Инициализирует IP-адрес адресом вида first\_octet.second\_octet.third\_octet.fourth\_octet.
Все компоненты адреса -- целые беззнаковые числа размером в байт.

### Конструктор IPAddress(uint32_t address)

В качестве адреса выступает 32-разрядное беззнаковое число, которое равносильно привычному
четырёх байтовому.

### Конструктор IPAddress(const uint8_t *address)

Конструктор получает на вход массив целых беззнаковых чисел. Этот массив должен иметь
четыре инициализированных элемента. Судя по текущей версии кода библиотеки, если
передать массив с большим числом элементов, то конструтор молча скопирует первые четыре
и проигнорирует все остальные. Если передать меньше, то дальнейшее поведение будет
ошибочным и непредсказуемым.

### Пример

Небольшой пример кода:

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

### Примечание

Внутри IPAddress адрес хранится в виде

``` arduino
	union {
		uint8_t bytes[4];
		uint32_t dword;
    } _address;
```

Таким образом, обе формы представления адреса эквивалентны и легко конвертируются
между собой.

---

[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
