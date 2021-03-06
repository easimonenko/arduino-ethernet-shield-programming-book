[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

# Библиотека Ethernet

[\[Библиотека Ethernet\]](/ethernet-library.markdown)

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

Метод _begin()_ настраивает сервер на прослушивание назначенного ему порта. Судя по коду
метода, он пытается занять все доступные (четыре) соединения (сокеты).

### Метод available()

Метод _available()_ проверяет, нет ли данных от полключённых клиентов, и если есть, то
возвращает объект клиента (класс EthernetClient). Если читать нечего, то возвращается
объект клиента, привязанный к сокету номер _MAX\_SOCK\_NUM_. Судя по коду метода,
если клиентов, доступных для чтения несколько, то всегда будет возвращаться тот, у 
которого наименьший номер. Вероятно, это может сделать возможной атаку DOS.

### Метод write()

Метод _write()_ отправляет данные **всем** подключённым клиентам. Метод представлен в 
двух формах:

* ```size_t EthernetServer::write(uint8_t b)```

* ```size_t EthernetServer::write(const uint8_t *buffer, size_t size)```

В первом случае клиентам оправляется указанный байт _b_. Во втором -- содержимое
буфера _buffer_ размером _size_ байт. Первый вариант всего лишь обёртка вокруг второго.
Метод возвращает количество отправленных байт всем клиентам. По идее, если отправка не
состоялась, то будет возвращен нуль; а если число оправленных байт не кратно _size_, то
во время отправки произошёл сбой и данные не были отправлены полностью.

### Метод print()

Метод _print()_ унаследован от класса _Print_ и подробно будет описан в соответствующей
главе. Этот метод позволяет отправлять клиентам данные различных типов строки, символы,
целые числа различной разрядности и числа с плавающей точкой, а также объекты с интерфейсом
_Printable_.

### Метод println()

Метод _println()_ делает всё тоже, что и метод print(), только добавляет в конец данных 
символ `\n`. Метод реализован как обёртка вокруг print(). В некоторых случаях целесообразнее
с точки зрения производительности использовать метод print() вместо println() просто
добавляя в конец данных символ `\n`.

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
