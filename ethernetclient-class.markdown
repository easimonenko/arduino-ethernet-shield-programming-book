[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

# Библиотека Ethernet

[\[Библиотека Ethernet\]](/ethernet-library.markdown)

## Класс EthernetClient

Класс _EthernetClient_ служит основой для реализации собственного сетевого клиента.
Также экземпляры этого класса связаны с клиентами объекта класса _EthernetServer_.
Этот класс наследует от класса _Client_ и реализует такие методы как begin(), write()
и available(). Рассмотрим их подробней.

### Конструктор EthernetClient()

Конструктор экземпляра класса _EthernetClient_ представлен в двух экземплярах:

``` arduino
    EthernetClient();
    EthernetClient(uint8_t sock);
```

Во втором случае на вход конструктору подаётся номер сокета _sock_, который является целым
числом от 0 до MAX_SOCK_NUM, который в нашем случае равен четырём. Если номер сокета не
задан, то он назначается равным MAX_SOCK_NUM.

### Метод connect()

Метод _connect()_ ...

### Метод available()

Метод _available()_ возвращает количество байт, доступных для чтения из сервера, к
которому он подключён.

``` arduino
    virtual int available();
```

### Метод write()

Метод _write()_ ...

### Метод print()

Метод _print()_ унаследован от класса _Print_ и подробно описывается в соответствующей
[главе](/print-class.markdown). Этот метод позволяет отправлять серверу данные различных
типов: строки, символы, целые числа различной разрядности и числа с плавающей точкой,
а также объекты с интерфейсом _Printable_.

### Метод println()

Метод _println()_ также унаследован от класса _Print_ и делает всё тоже, что и метод print(),
только добавляет в конец данных символ `\n`. Метод реализован как обёртка вокруг print().
В некоторых случаях целесообразнее с точки зрения производительности использовать метод
print() вместо println(), просто добавляя в конец данных символ `\n`.

### Пример

Ниже приведён пример простейшего сервера, который слушает порт 23 (telnet), читает, что ему
передаёт клиент, и возвращает ему это обратно.

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
