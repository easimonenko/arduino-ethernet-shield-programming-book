[\[К началу\]](/readme.markdown)

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

* [Класс IPAddress](/ipaddress-class.markdown)

* [Класс EthernetServer](/ethernetserver-class.markdown)

* [Класс EthernetClient](/ethernetclient-class.markdown)

Смотри также:

* [Библиотека SD](/sd-library.markdown)

* [Библиотека SPI](/spi-library.markdown)

* [Библиотека Core](/core-library.markdown)

---

[\[К началу\]](/readme.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
