---
date: 2024-09-24
tags:
  - Процедурне_програмування
  - Константи_та_рядки
---
Розглянемо наступну програму:
```cpp
#include <iostream>

int main()
{
    int x { 5 }; // x makes a copy of its initializer
    std::cout << x << '\n';

    return 0;
}
```
Коли виконується визначення для `x`, значення ініціалізації `5` копіюється у пам'ять, виділену для змінної `int x`. Для фундаментальних типів ініціалізація та копіювання змінної відбувається швидко.

Тепер розглянемо подібну програму:
```cpp
#include <iostream>
#include <string>

int main()
{
    std::string s{ "Hello, world!" }; // s makes a copy of its initializer
    std::cout << s << '\n';

    return 0;
}
```
При ініціалізації `s` у пам'ять, виділену для `std::string s`, копіюється рядковий літерал у стилі C `"Hello, world!"`. На відміну від фундаментальних типів, ініціалізація та копіювання `std::string` відбувається повільно.

У вищенаведеній програмі все, що ми робимо з `s`, це виводимо значення на консоль, а потім знищуємо `s`. По суті, ми створили копію `"Hello, world!"` просто для того, щоб надрукувати, а потім знищити цю копію. Це неефективно.

У цьому прикладі ми бачимо щось подібне:
```cpp
#include <iostream>
#include <string>

void printString(std::string str) // str makes a copy of its initializer
{
    std::cout << str << '\n';
}

int main()
{
    std::string s{ "Hello, world!" }; // s makes a copy of its initializer
    printString(s);

    return 0;
}
```
У цьому прикладі створюється дві копії рядка `"Hello, world!"` у стилі C: одна при ініціалізації `s` у функції `main()`, а інша при ініціалізації параметра `str` у функції `printString()`. Це дуже багато непотрібного копіювання лише для того, щоб надрукувати рядок!
## `std::string_view` `C++17`
Щоб вирішити проблему з дорогою ініціалізацією (або копіюванням) `std::string`, у C++17 було введено `std::string_view` (який знаходиться у заголовку `<string_view>`). `std::string_view` надає доступ лише для читання до існуючого рядка (рядка у стилі C, `std::string` або іншого `std::string_view`), не створюючи його копії. Доступ тільки для читання означає, що ми можемо отримати доступ до значення, яке переглядається, і використовувати його, але не можемо його змінити.

Наступний приклад ідентичний попередньому, за винятком того, що ми замінили `std::string` на `std::string_view`.
```cpp
#include <iostream>
#include <string_view> // C++17

// str provides read-only access to whatever argument is passed in
void printSV(std::string_view str) // now a std::string_view
{
    std::cout << str << '\n';
}

int main()
{
    std::string_view s{ "Hello, world!" }; // now a std::string_view
    printSV(s);

    return 0;
}
```
Ця програма видає той самий результат, що і попередня, але не робить копій рядка `"Hello, world!"`.

Коли ми ініціалізуємо `std::string_view s` рядковим літералом `"Hello, world!"` у стилі C, `s` надає доступ тільки для читання до `"Hello, world!"` без створення копії рядка. Коли ми передаємо `s` у `printSV()`, параметр `str` ініціалізується з `s`. Це дозволяє нам отримати доступ до `"Hello, world!"` через `str`, знову ж таки без створення копії рядка.
> [!tip]
> Надавайте перевагу `std::string_view` перед `std::string`, якщо вам потрібен рядок лише для читання, особливо для параметрів функцій.
## `std::string_view` може бути ініціалізовано багатьма різними типами рядків
Однією з приємних особливостей `std::string_view` є його гнучкість. Об'єкт `std::string_view` можна ініціалізувати рядком у стилі C, `std::string` або іншим `std::string_view`:
```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string_view s1 { "Hello, world!" }; // initialize with C-style string literal
    std::cout << s1 << '\n';

    std::string s{ "Hello, world!" };
    std::string_view s2 { s };  // initialize with std::string
    std::cout << s2 << '\n';

    std::string_view s3 { s2 }; // initialize with std::string_view
    std::cout << s3 << '\n';

    return 0;
}
```
## Параметри `std::string_view` прийматимуть багато різних типів рядкових аргументів
Як рядок у стилі C, так і `std::string` неявно перетворюються у `std::string_view`. Отже, параметр `std::string_view` прийматиме аргументи типу рядок у стилі C, `std::string` або `std::string_view`:
```cpp
#include <iostream>
#include <string>
#include <string_view>

void printSV(std::string_view str)
{
    std::cout << str << '\n';
}

int main()
{
    printSV("Hello, world!"); // call with C-style string literal

    std::string s2{ "Hello, world!" };
    printSV(s2); // call with std::string

    std::string_view s3 { s2 };
    printSV(s3); // call with std::string_view

    return 0;
}
```
## `std::string_view` не буде неявно перетворено у `std::string`
Оскільки `std::string` робить копію свого ініціалізатора (а це дорого), C++ не дозволяє неявне перетворення `std::string_view` у `std::string`. Це зроблено для того, щоб запобігти випадковій передачі аргументу `std::string_view` параметру `std::string` і ненавмисному створенню дорогої копії там, де така копія може бути непотрібною.

Однак, якщо це бажано, у нас є два варіанти:
1. Явно створити `std::string` з ініціалізатором `std::string_view` (це дозволено, оскільки це рідко робиться ненавмисно)
2. Перетворення існуючого `std::string_view` у `std::string` з використанням `static_cast`
У наступному прикладі показано обидва варіанти:
```cpp
#include <iostream>
#include <string>
#include <string_view>

void printString(std::string str)
{
	std::cout << str << '\n';
}

int main()
{
	std::string_view sv{ "Hello, world!" };

	// printString(sv);   // compile error: won't implicitly convert std::string_view to a std::string

	std::string s{ sv }; // okay: we can create std::string using std::string_view initializer
	printString(s);      // and call the function with the std::string

	printString(static_cast<std::string>(sv)); // okay: we can explicitly cast a std::string_view to a std::string

	return 0;
}
```
## Присвоєння змінює те, що переглядає `std::string_view`
Присвоєння нового рядка до `std::string_view` призводить до того, що `std::string_view` переглядає новий рядок. Це ніяк не змінює попередній рядок, який переглядається.

Наступний приклад ілюструє це:
```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string name { "Alex" };
    std::string_view sv { name }; // sv is now viewing name
    std::cout << sv << '\n'; // prints Alex

    sv = "John"; // sv is now viewing "John" (does not change name)
    std::cout << sv << '\n'; // prints John

    std::cout << name << '\n'; // prints Alex

    return 0;
}
```
У наведеному вище прикладі `sv = "John"` призводить до того, що `sv` тепер переглядає рядок `"John"`. Це не змінює значення, що зберігається за іменем (яке все ще залишається `"Alex"`).
## Літерали для `std::string_view`
Рядкові літерали у подвійних лапках за замовчуванням є рядковими літералами у стилі C. Ми можемо створювати рядкові літерали типу `std::string_view`, використовуючи суфікс `sv` після рядкового літерала у подвійних лапках. Суфікс `sv` має бути у нижньому регістрі.
```cpp
#include <iostream>
#include <string>      // for std::string
#include <string_view> // for std::string_view

int main()
{
    using namespace std::string_literals;      // access the s suffix
    using namespace std::string_view_literals; // access the sv suffix

    std::cout << "foo\n";   // no suffix is a C-style string literal
    std::cout << "goo\n"s;  // s suffix is a std::string literal
    std::cout << "moo\n"sv; // sv suffix is a std::string_view literal

    return 0;
}
```
Можна ініціалізувати об'єкт `std::string_view` рядковим літералом у стилі C (не обов'язково ініціалізувати його літералом `std::string_view`).

Проте, ініціалізація `std::string_view` за допомогою літералу `std::string_view` не спричинить проблем (оскільки такі літерали насправді є замаскованими рядковими літералами у стилі C).
## constexpr `std::string_view`
На відміну від `std::string`, `std::string_view` має повну підтримку `constexpr`:
```cpp
#include <iostream>
#include <string_view>

int main()
{
    constexpr std::string_view s{ "Hello, world!" }; // s is a string symbolic constant
    std::cout << s << '\n'; // s will be replaced with "Hello, world!" at compile-time

    return 0;
}
```
Це робить `constexpr std::string_view` кращим вибором, коли потрібні рядкові символьні константи.

Ми продовжимо обговорення `std::string_view` у наступному уроці.