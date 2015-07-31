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

Далее:

* [Объект Ethernet](/ethernet-object.markdown)

* [Класс IPAddress](/ipaddress.markdown)

* [Класс EthernetServer](/ethernet-server-class.markdown)

Смотри также:

* [Библиотека SD](/sd-library.markdown)

* [Библиотека SPI](/spi-library.markdown)

* [Библиотека Print](/print-library.markdown)


## Класс Sever

Класс _Server_ является базовым абстрактным классом в то числе и для описываемых здесь ниже.
Объекты от этого класса непосредственно не создают. Класс _Server_ наследует от класса _Print_.
Это означает, что у класса _Server_ есть методы класса _Print_ такие как _print()_ и _println()_.
Класс _Print_ будет рассмотрен в одной из следующих глав.

## Класс EthernetServer

Класс _EthernetServer_ служит основой для реализации собственного сетевого сервера.
Этот класс наследует от класса _Server_ и реализует такие методы как begin(), write()
и available(). Рассмотрим их подробней.

### Конструктор EthernetServer()

Конструктор экземпляра класса _EthernetServer_ представлен в единственном экземпляре:

``` arduino
	EthernetServer(uint16_t port);
```

На вход конструктору подаётся номер прослушиваемого порта _port_, который является целым
16-разрядным беззнаковым значением.

### Метод begin()

...

### Метод available()

...

### Метод write()

...

### Метод print()

...

### Метод println()

...

### Пример

Ниже приведён пример простейшего сервера, который слушает порт 23 (telnet), читает, что ему
передаёт клиент и возвращает ему это обратно.

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

[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
