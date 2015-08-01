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
