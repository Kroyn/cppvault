## Встановлення
1. Заходим на офіційний сайт [Visual Studio](https://visualstudio.microsoft.com/), і нажимаем кнопку Download Visual Studio.
![Pasted image 20240909041609.png](./images/Pasted%20image%2020240909041609.png)
2. Після нажаться на кнопку у вас має початись завантаження інсталера Visual Studio.
![Pasted image 20240909041753.png](./images/Pasted%20image%2020240909041753.png)
3. Після того як у вас встановиться запустите його, якщо після запуска у вас так-же як на фото то у вас все добре, якщо так нажимаем Continue.
![Pasted image 20240909041958.png](./images/Pasted%20image%2020240909041958.png)
4. Після нажатья у вас почнеться завантаження, зачекайте і у вас з'явиться таке вікно.
![Pasted image 20240909042121.png](./images/Pasted%20image%2020240909042121.png)
5. Якщо ви новичок в С++ то раджу вибрати тільки те що на фото.
![Pasted image 20240909042539.png](./images/Pasted%20image%2020240909042539.png)
Пока вам не стоїть турбуватись що вони всі означають, с времени ви поймети що вони роблять і для чого
6. Після вибору і нажатья на Install, у вас почнеться завантаження самого Visual Studio.
![Pasted image 20240909042756.png](./images/Pasted%20image%2020240909042756.png)
Чекаемо...
7. Після завантаження у вас буде таке.
![Pasted image 20240909043455.png](./images/Pasted%20image%2020240909043455.png)
Тут по вашему бажаню можете зразу запустити Visual Studio.

Якщо ви зробили всі вірно, вітаю ви встановили Visual Studio!
![Pasted image 20240909043644.png](./images/Pasted%20image%2020240909043644.png)
## Створення проекту
1. Натискаемо Create a new project.
![Pasted image 20240909043811.png](./images/Pasted%20image%2020240909043811.png)
2. Тут ми повинні вибрати шаблон проекту, вибираемо Console App і натискаемо далі.
![Pasted image 20240909043953.png](./images/Pasted%20image%2020240909043953.png)
3. Далі нас просять назву проекту.
Project name: вписуем назву проекта.
Location: можете указати место розположение проекта.
Solution name: це коротше кажучи контейнер для організації та керування проектами, можете залишити таку же назву як у проекта.
![Pasted image 20240909044450.png](./images/Pasted%20image%2020240909044450.png)

Вітаю ви сторили проект!
![Pasted image 20240909044518.png](./images/Pasted%20image%2020240909044518.png)
## Як запустити программу в VS
Просто натискайте Ctrl + F5.

або нажати на цю кнопку:
![Pasted image 20240909044945.png](./images/Pasted%20image%2020240909044945.png)

Якщо все вірно у вас буде таке:
![Pasted image 20240909044811.png](./images/Pasted%20image%2020240909044811.png)

## Налаштування проекта
### Зміни тип компіляції
Ви можете змінити тип компіляції, наприклад архітектуру, це робить там де на фото:
![Pasted image 20240909045153.png](./images/Pasted%20image%2020240909045153.png)
Режим Debug: це для налагодження, краще залишайтесь на цьому режиме.
Режим Release: режим випуску, це якщо ви хочете скоплювати вашу программу до випоску, полезно якщо вже закінчили написання своей программи і хочете поширити.

x86/x64: це типи архітектури, в наш час краще вибирати тільки x64, але ви можете вибрати x86 щоб прискорити процес компіляції.
### Зміни стандарту
По стандарту в новом проете у вас буде C++14, якщо хочете змінити на інший, натискаемо правою кнопною на назву проекту, і вибираемо Properties.
![Pasted image 20240909045829.png](./images/Pasted%20image%2020240909045829.png)

У вас з'явиться вікно, в вкладці General шукаем С++ Language Standard, і вибираемо желаемий(раджу використовувати C++20).
![Pasted image 20240909050017.png](./images/Pasted%20image%2020240909050017.png)
Після цього натиске Apply і OK.

Далі буде...