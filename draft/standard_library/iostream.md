## `iostream`: Введення/виведення даних у C++
`iostream` є стандартною бібліотекою C++, яка надає засоби для введення та виведення даних на консоль, файли та інші потоки. Вона забезпечує об'єктно-орієнтований підхід до введення/виведення, що робить його більш гнучким і зручним у використанні порівняно зі старішими методами.

## Основні компоненти `iostream`
### `std::cout`
Стандартний вихідний потік, зазвичай пов'язаний з консоллю.

Приклад:
```cpp
	#include <iostream>
	
	int main()
	{
		std::cout << "Hello World\n";
		return 0;
	}
```
Виводить:
```
Hello World
```

### `std::cin`
Стандартний вхідний потік, зазвичай пов'язаний з клавіатурою.

Приклад:
```cpp
#include <iostream>

int main()
{
	std::cout << "Enter a number: ";
	int number{};
	std::cin >> number;

	std::cout << "You enter: " << number << '\n';

	return 0;
}
```
Виводить:
```
Enter a number: 5
You enter: 5
```

### `std::cerr`
Стандартний потік помилок, зазвичай пов'язаний з консоллю.

Головна відмінисть від `std::cout` те що він не буфезується

> [!tip]
> Використовуйте його якщо треба з'ясувати проблему
## Маніпулятори
### `std::endl`
Закінчити строку і перейти до наступної строки.

Приклад:
```cpp
#include <iostream>

int main()
{
    std::cout << "Hello my name is" << std::endl;
    std::cout << "Ivan" << std::endl;

    return 0;
}
```

> [!tip]
> Я раджу використовувати `'\n'` замість `std::endl`, оскільки `std::endl` очищає буфер перед виконанням, що може сповільнити роботу програми.

### `std::boolalpha`/`std::noboolalpha`
Виводить замість `0` і `1`, `false` і `true`.

```cpp
	std::cout << std::boolalpha;
	std::cout << false << '\n';
	std::cout << true << '\n';
```
> [!caution]
> Увімкнення `std::boolalpha` для вводу дозволить приймати лише малі літери `false` або `true`. Варіації з великими літерами не будуть прийняті. `0` та `1` також більше не прийматимуться.
## `std::setprecision();`
Використовується для керування кількістю цифр, що виводяться під час друку чисел з плаваючою комою.

Приклад:
```cpp
#include <iostream>
#include <iomanip>

int main() {
    double pi = 3.14159;

    std::cout << "Value of pi: " << pi << '\n';

    std::cout << "Value of pi (fixed, 3 decimal places): " << std::fixed << std::setprecision(3) << pi << '\n';

    std::cout << "Value of pi (scientific, 4 significant digits): " << std::scientific << std::setprecision(4) << pi << '\n';

    return 0;
}
```
Виход:
```
Value of pi: 3.14159
Value of pi (fixed, 3 decimal places): 3.142
Value of pi (scientific, 4 significant digits): 3.1416e+00
```

### `std::flush`
Примусово очищає буфер виведення без додавання нового рядка.
```cpp
std::cout << "Hello" << std::flush;
```

### `std::setw()`
Встановлює ширину поля для наступного елемента.
```cpp
std::cout << std::setw(10) << 123 << std::endl;
```
### `std::setfill()`
Встановлює символ для заповнення порожніх місць.
```cpp
std::cout << std::setw(10) << std::setfill('*') << 123 << std::endl;
```
### `std::left`
Вирівнює виведення по лівому краю.
```cpp
std::cout << std::left << std::setw(10) << 123 << std::endl;
```
### `std::right`
Вирівнює виведення по правому краю.
```cpp
std::cout << std::right << std::setw(10) << 123 << std::endl;
```
### `std::fixed`
Встановлює фіксований формат для відображення чисел з плаваючою точкою.
```cpp
std::cout << std::fixed << 3.14159 << std::endl;
```
### `std::scientific`
Встановлює науковий формат для чисел з плаваючою точкою.
```cpp
std::cout << std::scientific << 3.14159 << std::endl;
```
### `std::hex`
Встановлює шістнадцяткову систему числення для виводу чисел.
```cpp
std::cout << std::hex << 255 << std::endl;  // виведе "ff"
```
### `std::dec`
Встановлює десяткову систему числення.
```cpp
std::cout << std::dec << 255 << std::endl;
```
### `std::oct`
Встановлює вісімкову систему числення.
```cpp
std::cout << std::oct << 255 << std::endl;  // виведе "377"
```
### `std::showpoint`
Примусово відображає десяткову крапку навіть для цілих чисел.
```cpp
std::cout << std::showpoint << 123.0 << std::endl;
```
### `std::noshowpoint`
Cкасовує примусове відображення десяткової крапки.
```cpp
std::cout << std::noshowpoint << 123.0 << std::endl;
```
### `std::uppercase` / `std::nouppercase`
Змінює регістр символів у шістнадцяткових числах (A-F).
```cpp
std::cout << std::uppercase << std::hex << 255 << std::endl;  // "FF"
```
## Маніпулятори для вводу:
### `std::ws`
Пропускає пробіли у вводі.
```cpp
std::cin >> std::ws >> input;
```
### `std::skipws` / `std::noskipws`
Дозволяє пропускати або не пропускати пробіли під час вводу.
```cpp
std::cin >> std::noskipws >> input;
```
## Додатково
### Використання `<format>` C++20
У C++20 ми маємо кращі можливості для друку двійкових файлів за допомогою нової бібліотеки форматів.
```cpp
#include <format> // C++20
#include <iostream>

int main()
{
    std::cout << std::format("{:b}\n", 0b1010);  // C++20, {:b} formats the argument as binary digits
    std::cout << std::format("{:#b}\n", 0b1010); // C++20, {:#b} formats the argument as 0b-prefixed binary digits

	return 0;
}
```
Це виводе:
```
1010
0b1010
```
### Використання `<print>` C++23
У C++23 ми маємо кращі можливості для друку двійкових файлів за допомогою нової бібліотеки форматів (C++20) та бібліотеки друку (C++23):
```cpp
#include <format> // C++20
#include <iostream>
#include <print> // C++23

int main()
{
    std::cout << std::format("{:b}\n", 0b1010);  // C++20, {:b} formats the argument as binary digits
    std::cout << std::format("{:#b}\n", 0b1010); // C++20, {:#b} formats the argument as 0b-prefixed binary digits

    std::println("{:b} {:#b}", 0b1010, 0b1010);  // C++23, format/print two arguments (same as above) and a newline

    return 0;
}

```
Це виводе:
```
1010
0b1010
1010 0b1010
```