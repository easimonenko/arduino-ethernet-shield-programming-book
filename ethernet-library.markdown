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

Рассмотрим передаваемые параметры подробней.

- _mac_: MAC-адрес Ethernet Shield; представляет из себя массив из шести байт.

- _ip_: IP-адрес Ethernet Sheild; представляет из себя массив из четырёх байт.

- _dns_: IP-адрес DNS-сервера; представляет из себя массив из четырёх байт;
	если не задан, то IP-адрес содержит в последнем октете 1.

- _gateway_: IP-адрес шлюза; представляет из себя массив из четырёх байт;
	если не задан, то IP-адрес содержит в последнем октете 1.

- _subnet_: маска подсети; представляет из себя массив из четырёх байт;
	по умолчанию это 255.255.255.0.

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

Небольшой пример кода с методом Ethernet.localIP():

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
	}

	void loop() {
	}
```

### Ethernet.maintain()

Метод _Ethernet.maintain()_ позволяет перепривязать или обновить выданный DHCP-сервером адрес.
Метод не получает никаких параметров и возвращает одно из следующих значений типа int:

* 0: ничего не получено;

* 1: обновление неуспешно;

* 2: обновление успешно;

* 3: перепривязка неуспешна;

* 4: перепривязка успешна.

---

[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
