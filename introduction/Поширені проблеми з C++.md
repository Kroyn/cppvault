# Чому не працює **кириллиця**?

Коли ви вводите це:

```cpp
#include <iostream>

int main()
{
	std::cout << "Привіт світ!";
}
```

Після компіляцію у вас вивовить таке:

```
?????? ????!
```

Або щось інше, але не те що ви хотіли.

Але чому не працює? Все в кодування, у С++ за замовчуванням використовується **ASCII** кодування, який не пітримує кириличні символи.

## Як виправити?

Існує кілька виришення.

### Перше виправлення.

Перший варіант виправлення це використовувати бібліотеку `<windows.h>`:

```cpp
#include <iostream>
#include <windows.h>

int main() {
    SetConsoleOutputCP(1251);
    SetConsoleCP(1251);

    std::cout << "Привіт світ!";

    return 0;
}
```

Але все-ж може не виводити, тут може допогти використовувати `std::wcout`:

```cpp
#include <iostream>
#include <windows.h>

int main() {
    SetConsoleOutputCP(1251);
    SetConsoleCP(1251);

    std::wcout << L"Привіт, світе!";

    return 0;
}
```

Все що више може не допомогти, інший варіант є більш шансів:

```cpp
#include <iostream>
#include <Windows.h>

int main() {
    SetConsoleOutputCP(1251);
    SetConsoleCP(1251);

    SetConsoleOutputCP(CP_UTF8);
    SetConsoleCP(CP_UTF8);

    std::cout << "Привіт, світ!";

    return 0;
}
```

### Друге виправлення.

Другий варіант правллення це використовувати бібліотеку `<locale>`:

```cpp
#include <iostream>
#include <locale>

int main() {
    std::locale::global(std::locale("uk_UA.UTF-8"));
    std::cout << "Привіт, світ!";

    return 0;
}
```

### Третє виправлення.

```cpp
#include <iostream>

int main() {
    system("chcp 1251>nul");

    std::cout << "Привіт, світ!";

    return 0;
}
```