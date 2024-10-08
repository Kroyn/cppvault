---
date: 2024-09-08
tags:
  - Процедурне_програмування
  - Фундаментальні_типи_дани
---
Розглянемо випадок, коли ви збираєтеся піти на ринок, а ваш сусід каже вам: "Якщо у них є полуниця на розпродажі, купіть її". Це умовне висловлювання, яке означає, що ви виконаєте певну дію ("купи"), тільки якщо умова ("на ринку є полуниця") буде істинною.

Такі умови є поширеним явищем у програмуванні, оскільки вони дозволяють нам реалізовувати умовну поведінку у наших програмах. Найпростіший тип умовного оператора в C++ називається оператором `if`. Оператор if дозволяє нам виконати один (або декілька) рядків коду, тільки якщо виконується деяка умова.

Найпростіший оператор if має наступний вигляд:
```
if (condition) true_statement;
```
Для зручності читання це частіше пишуть наступним чином:
```
if (condition)
    true_statement;
```
Умова (також звана умовним виразом) - це вираз, який обчислює булеве значення.

Якщо умова оператора `if` набуває логічного значення `true`, то виконується оператор `true_statement`. Якщо умова натомість обчислює булеве значення `false`, то оператор `true_statement` пропускається.
## Приклад програми з використанням інструкції `if`
Дана наступна програма:
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    if (x == 0)
        std::cout << "The value is zero\n";

    return 0;
}
```
Ось результати одного запуску цієї програми:
```
Enter an integer: 0
The value is zero
```
Давайте розглянемо, як це працює більш детально.

Спочатку користувач вводить ціле число. Потім обчислюється умова `x == 0`. Оператор рівності (`==`) використовується для перевірки рівності двох значень. `operator==` повертає `true`, якщо операнди рівні, і `false`, якщо ні. Оскільки `x` має значення `0`, а `0 == 0` є істинним, цей вираз обчислюється як `true`.

Оскільки умова набула значення true, виконується наступний оператор, який виводить значення нуль.

Ось ще один запуск цієї програми:
```
Enter an integer: 5
```
У цьому випадку `x == 0` обчислюється як `false`. Наступний оператор пропускається, програма завершується і більше нічого не виводиться.

> [!caution]
> Якщо оператори лише умовно виконують один оператор.
## If-else
З огляду на наведений вище приклад, що, якщо ми хочемо сказати користувачеві, що введене ним число відмінне від нуля?

Ми могли б написати щось на зразок цього:
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    if (x == 0)
        std::cout << "The value is zero\n";
    if (x != 0)
        std::cout << "The value is non-zero\n";

    return 0;
}
```
Або це:
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    bool zero { (x == 0) };
    if (zero)
        std::cout << "The value is zero\n";
    if (!zero)
        std::cout << "The value is non-zero\n";

    return 0;
}
```
Обидві ці програми є складнішими, ніж потрібно. Замість цього ми можемо використовувати альтернативну форму інструкції `if`, яка називається i`f-else`. `If-else` має наступний вигляд:
```
if (condition)
    true_statement;
else
    false_statement;
```
Якщо умова обчислюється як булева істина, виконується `true_statement`. В іншому випадку виконується оператор `false_statement`.

Давайте змінимо нашу попередню програму, щоб використовувати `if-else`.
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    if (x == 0)
        std::cout << "The value is zero\n";
    else
        std::cout << "The value is non-zero\n";

    return 0;
}
```
Тепер наша програма видасть наступний результат:
```
Enter an integer: 0
The value is zero
```
```
Enter an integer: 5
The value is non-zero
```
## Ланцюгові оператори `if`
Іноді нам потрібно перевірити істинність або хибність кількох послідовних дій. Ми можемо зробити це, приєднавши інструкцію `if` (або `if-else`) до попередньої інструкції `if-else`, ось так:
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    if (x > 0)
        std::cout << "The value is positive\n";
    else if (x < 0)
        std::cout << "The value is negative\n";
    else
        std::cout << "The value is zero\n";

    return 0;
}
```
Оператор менше ніж (`<`) використовується для перевірки того, чи є одне значення меншим за інше. Аналогічно, оператор більше (`>`) використовується для перевірки того, чи є одне значення більшим за інше. Обидва оператори повертають логічні значення.

Нижче наведено результати декількох запусків цієї програми:
```
Enter an integer: 4
The value is positive
```
```
Enter an integer: -3
The value is negative
```
```
Enter an integer: 0
The value is zero
```
Зверніть увагу, що ви можете з'єднувати оператори `if` стільки разів, скільки умов ви хочете оцінити. У тесті ми побачимо приклад, де це може бути корисним.
## Булеві значення повернення та оператори if
```cpp
#include <iostream>

// returns true if x and y are equal, false otherwise
bool isEqual(int x, int y)
{
    return x == y; // operator== returns true if x equals y, and false otherwise
}

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    std::cout << "Enter another integer: ";
    int y {};
    std::cin >> y;

    std::cout << std::boolalpha; // print bools as true or false

    std::cout << x << " and " << y << " are equal? ";
    std::cout << isEqual(x, y); // will return true or false

    std::cout << '\n';

    return 0;
}
```
Давайте вдосконалимо цю програму за допомогою інструкції `if`:
```cpp
#include <iostream>

// returns true if x and y are equal, false otherwise
bool isEqual(int x, int y)
{
    return x == y; // operator== returns true if x equals y, and false otherwise
}

int main()
{
    std::cout << "Enter an integer: ";
    int x {};
    std::cin >> x;

    std::cout << "Enter another integer: ";
    int y {};
    std::cin >> y;

    if (isEqual(x, y))
        std::cout << x << " and " << y << " are equal\n";
    else
        std::cout << x << " and " << y << " are not equal\n";

    return 0;
}
```
Два запуски цієї програми:
```
Enter an integer: 5
Enter another integer: 5
5 and 5 are equal
```
```
Enter an integer: 6
Enter another integer: 4
6 and 4 are not equal
```
У цьому випадку наш умовний вираз - це просто виклик функції `isEqual`, яка повертає булеве значення.
## Небулеві умови
У всіх наведених вище прикладах наші умови були або булевими значеннями (істинними чи хибними), або булевими змінними, або функціями, які повертають булеві значення. Що станеться, якщо ваша умова - це вираз, який не перетворюється на булеве значення?

У такому випадку умовний вираз перетворюється на булеве значення: ненульові значення перетворюються на булеву істину, а нульові - на булеву хибність.

Тому, якщо ми робимо щось на кшталт цього:
```cpp
#include <iostream>

int main()
{
    if (4) // nonsensical, but for the sake of example...
        std::cout << "hi\n";
    else
        std::cout << "bye\n";

    return 0;
}
```
Буде виведено "hi", оскільки `4` є ненульовим значенням, яке перетворюється на булеву істину, що призведе до виконання оператора, приєднаного до `if`.
## If-заяви та дострокове повернення
Оператор повернення, який не є останнім оператором у функції, називається **раннім поверненням**. Такий оператор призводить до того, що функція повернеться до викликаючого користувача після виконання оператора return (до того, як функція інакше повернулася б до викликаючого користувача, отже, "достроково").

Безумовне дострокове повернення не є корисним:
```cpp
void print()
{
    std::cout << "A" << '\n';

    return; // the function will always return to the caller here

    std::cout << "B" << '\n'; // this will never be printed
}
```
Оскільки `std::cout << "B" << '\n';` ніколи не буде виконано, ми можемо видалити його, і тоді наш оператор return вже не буде передчасним.

Однак, у поєднанні з if-інструкціями, раннє повернення дає змогу обумовити значення, що повертається нашою функцією.
```cpp
#include <iostream>

// returns the absolute value of x
int abs(int x)
{
    if (x < 0)
        return -x; // early return (only when x < 0)

    return x;
}

int main()
{
    std::cout << abs(4) << '\n'; // prints 4
    std::cout << abs(-3) << '\n'; // prints 3

    return 0;
}
```
Коли викликається `abs(4)`, `x` має значення `4`. якщо `(x < 0)` - `false`, то дострокове повернення не виконується. Функція повертає `x` (значення `4`) користувачеві в кінці функції.

Коли викликається `abs(-3)`, `x` має значення `-3`. якщо `(x < 0)` істинно, то виконується дострокове повернення. Функція повертає `-x` (значення `3`) користувачеві, який її викликав.

Історично ранні повернення не схвалювалися. Однак у сучасному програмуванні вони є більш прийнятними, особливо коли їх можна використати для спрощення функції або для дострокового переривання функції через певні умови помилки.