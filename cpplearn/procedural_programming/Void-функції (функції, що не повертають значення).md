---
date: 2024-09-02
tags:
  - Процедурне_програмування
  - Основи
---
## Значення, що повертаються у вигляді void
Функції не зобов'язані повертати значення тому, хто їх викликає. Щоб вказати компілятору, що функція не повертає значення, використовується тип повернення void. Наприклад:

```cpp
#include <iostream>

// void means the function does not return a value to the caller
void printHi()
{
    std::cout << "Hi" << '\\n';

    // This function does not return a value so no return statement is needed
}

int main()
{
    printHi(); // okay: function printHi() is called, no value is returned

    return 0;
}
```

У наведеному вище прикладі функція `printHi` має корисну поведінку (вона виводить "Hi"), але їй не потрібно нічого повертати користувачеві. Тому функції `printHi` присвоєно тип повернення void.

Коли main викликає `printHi`, код у `printHi` виконується, і виводиться "Hi". Після завершення роботи `printHi` керування повертається до `main`, і програма продовжує роботу.

Функція, яка не повертає значення, називається функцією, що не повертає значення (або функцією void).
## Void-функції не потребують оператора return
Функція void автоматично повернеться до викликувача в кінці функції. Оператор return не потрібен.

У функції void можна використовувати інструкцію return (без значення, що повертається) - така інструкція призведе до повернення функції викликаючому користувачеві в точці, де виконується інструкція return. Це те саме, що відбувається в кінці функції у будь-якому випадку. Отже, розміщення порожнього оператора return в кінці void-функції є надлишковим:

```cpp
#include <iostream>

// void means the function does not return a value to the caller
void printHi()
{
    std::cout << "Hi" << '\\n';

    return; // tell compiler to return to the caller -- this is redundant since the return will happen at the end of the function anyway!
} // function will return to caller here

int main()
{
    printHi();

    return 0;
}
```

> [!success] 
> Не ставте оператор return в кінці функції, що не повертає значення.
## Функції-пустоти не можна використовувати у виразах, які вимагають значення
Деякі типи виразів вимагають значень. Наприклад:

```cpp
#include <iostream>

int main()
{
    std::cout << 5; // ok: 5 is a literal value that we're sending to the console to be printed
    std::cout << ;  // compile error: no value provided

    return 0;
}
```

У вищенаведеній програмі значення, яке потрібно вивести, має бути вказано у правій частині `std::cout <<`. Якщо значення не вказано, компілятор видасть синтаксичну помилку. Оскільки другий виклик `std::cout` не містить значення для виведення, це призводить до помилки.

Тепер розглянемо наступну програму:

```cpp
#include <iostream>

// void means the function does not return a value to the caller
void printHi()
{
    std::cout << "Hi" << '\\n';
}

int main()
{
    printHi(); // okay: function printHi() is called, no value is returned

    std::cout << printHi(); // compile error

    return 0;
}
```

Перший виклик `printHi()` викликається у контексті, який не вимагає значення. Оскільки функція не повертає значення, це нормально.

Другий виклик функції `printHi()` навіть не скомпілюється. Функція `printHi` має тип повернення void, тобто вона не повертає значення. Однак, цей оператор намагається відправити значення, що повертається функцією `printHi`, до `std::cout` для виведення. `std::cout` не знає, як з цим впоратися (яке значення вивести на екран?). Отже, компілятор позначить це як помилку. Вам потрібно закоментувати цей рядок коду для того, щоб ваш код було скомпільовано.


> [!NOTE]
> > [!NOTE] 
> > Деякі твердження вимагають надання значень, а інші - ні.
> 
> Коли ми маємо оператор, який складається лише з виклику функції (наприклад, перший `printHi()` у наведеному вище прикладі), ми викликаємо функцію для її поведінки, а не для значення, яке вона повертає. У цьому випадку ми можемо викликати або функцію, яка не повертає значення, або викликати функцію, яка повертає значення, і просто ігнорувати значення, що повертається.
> 
> Коли ми викликаємо функцію в контексті, який вимагає значення (наприклад, `std::cout`), значення має бути надано. У такому контексті ми можемо викликати тільки функції, що повертають значення.
```cpp
#include <iostream>

// Function that does not return a value
void returnNothing()
{
}

// Function that returns a value
int returnFive()
{
    return 5;
}

int main()
{
    // When calling a function by itself, no value is required
    returnNothing(); // ok: we can call a function that does not return a value
    returnFive();    // ok: we can call a function that returns a value, and ignore that return value

    // When calling a function in a context that requires a value (like std::cout)
    std::cout << returnFive();    // ok: we can call a function that returns a value, and the value will be used
    std::cout << returnNothing(); // compile error: we can't call a function that returns void in this context

    return 0;
}
```
## Повернення значення з функції void є помилкою компіляції
Спроба повернути значення з функції, яка не повертає значення, призведе до помилки компіляції:

```cpp
void printHi() // This function is non-value returning
{
    std::cout << "In printHi()" << '\\n';

    return 5; // compile error: we're trying to return a value
}
```