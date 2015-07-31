[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

# Библиотека Ethernet

[\[Библиотека Ethernet\]](/ethernet-library.markdown)

## Класс IPAddress

Класс _IPAddress_ предоставляет обёртку для IP-адресов.

### Подключение

Если библиотека Ethernet подключена, то для использования IPAddress ничего больше подключать
не нужно. В противном случае подключайте так:

``` arduino
	#include "IPAddress.h"
```

### Конструктор IPAddress()

Конструктор IPAddress() существует в нескольких формах:

``` arduino
	IPAddress()
	IPAddress(uint8\_t first\_octet, uint8\_t second\_octet, uint8\_t third\_octet, uint8\_t fourth\_octet)
	IPAddress(uint32_t address)
	IPAddress(const uint8_t *address)
```

Рассмотрим каждый поподробней.

Конструктор _IPAddress()_ инициализирует IP-адрес нулевым значением (адрес 0.0.0.0).

Конструктор _IPAddress(uint8\_t first\_octet, uint8\_t second\_octet, uint8\_t third\_octet, uint8\_t fourth\_octet)_
инициализирует IP-адрес адресом вида first\_octet.second\_octet.third\_octet.fourth\_octet.
Все компоненты адреса -- целые беззнаковые числа размером в байт.

Конструктор _IPAddress(uint32\_t address)_ получает в качестве адреса 32-разрядное
беззнаковое число, которое равносильно привычному четырёх байтовому.

Конструктор _IPAddress(const uint8\_t *address)_ получает на вход массив целых
беззнаковых чисел. Этот массив должен иметь четыре инициализированных элемента.
Судя по текущей версии кода библиотеки, если передать массив с большим числом элементов,
то конструтор молча скопирует первые четыре и проигнорирует все остальные. Если передать
меньше, то дальнейшее поведение будет ошибочным и непредсказуемым.

### Метод printTo()

Метод _printTo()_ реализует интерфейс _Printable_ и объявлен следующим образом:

``` arduino
	virtual size_t printTo(Print& p) const;
```

В основном этот метод используется библиотечными методами _print()_ и _println()_ для 
получения текстового представления объекта (класс _Print_).

### Оператор uint32\_t()

Оператор _uint32\_t()_ объявлен следующим образом:

``` arduino
	operator uint32_t() const { return _address.dword; };
```

Оператор _uint32\_t()_ служит преобразованию адреса из одной формы представления в другую.

### Оператор сравнения (==)

Оператор сравнения (==) объявлен в двух формах:

``` arduino
	bool operator==(const IPAddress& addr) const { return _address.dword == addr._address.dword; };
    bool operator==(const uint8_t* addr) const;
```

Оператор позволяет сравнивать два объекта IPAddress или объект IPAdrress и IP-адрес в форме
массива из четырёх чисел.

### Оператор присваивания (=)

Оператор присваивания (=) представлен в двух формах:

``` arduino
	IPAddress& operator=(const uint8_t *address);
    IPAddress& operator=(uint32_t address);
```

Благодаря этим двум операторам, мы можем задавать IP-адрес в форме массива из четырёх
чисел или в форме четырёх байтового числа.

### Оператор индексации ([])

Оператор индексации позволяет обращаться к каждой из четырёх компонент IP-адреса
по отдельности.

```arduino
	uint8_t operator[](int index) const { return _address.bytes[index]; };
    uint8_t& operator[](int index) { return _address.bytes[index]; };
```

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

Смотри также:

* [Объект Ethernet](/ethernet-object.markdown)

* [Класс EthernetServer](/ethernetserver-class.markdown)

* [Класс EthernetClient](/ethernetclient-class.markdown)

---

[\[К началу\]](/readme.markdown) | [\[Библиотека SD\]](/sd-library.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
