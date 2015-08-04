[\[К началу\]](/readme.markdown)

---

# Класс Print

Класс _Print_ является базовым классом для многих классов Arduino, в том числе
и для таких как EthernetServer, EthernetClient. Цель данного класса -- предоставить
набор методов символьного ввода-вывода верхнего уровня. Наследующий ему класс
должен реализовать метод write(), который собственно и осуществляет ввод-вывод.

``` arduino
	virtual size_t write(uint8_t) = 0;
```

Вот как объявлены основные методы класса Print:

``` arduino
	size_t print(const String &);
    size_t print(const char[]);
    size_t print(char);
    size_t print(unsigned char, int = DEC);
    size_t print(int, int = DEC);
    size_t print(unsigned int, int = DEC);
    size_t print(long, int = DEC);
    size_t print(unsigned long, int = DEC);
    size_t print(double, int = 2);
    size_t print(const Printable&);
```

Из этого списка видно, что класс умеет выводить в символьном виде данные следующих
типов: String (строка), массив char (строка Си), char (символ), байт (восемь бит),
слово (16 бит), длинное слово (32 бит), число с плавающей точкой (double)
и объекты с интерфейсом Printable.

По умолчанию целые числа выводятся в десятичной системе счисления, но её можно изменить на
HEX (шестнадцатиричная), OCT (восьмеричная) и BIN (двоичная).

``` arduino
	#define DEC 10
	#define HEX 16
	#define OCT 8
	#define BIN 2
```

Объект с интерфейсом Printable должен реализовать метод _printTo()_.

Предоставляется также аналогичный набор методов _println()_, единственное
отличие которых заключается в добавлении в конец вывода символа `\n`.
Для этой цели есть также отдельный метод _println(void)_ (без параметров),
который просто выводит символ `\n`.

---

[\[К началу\]](/readme.markdown)

---

(c) 2015, Симоненко Евгений А. <easimonenko@mail.ru>
