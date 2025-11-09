## Лабораторно-практична робота №3
### Розробка та тестування захищеного REST API на Node.js та Express.

Даний API призначений для показу роботи програми на серверній частині за допомогою Node.js та Express, <br>
показу основних аспектів та принципів роботи RESTful API для безпечних серверних застосунків: аутентифікацію, авторизацію за ролями, логування запитів та обробку HTTP-статусів. <br>

## Інструкції з використання команд
### npm install<br>
Використовується для встановленння всіх залежностей, які необхідні для проєкту<br><br>

Перед застосуванням команди треба: <br>
1. Вибрати де буде знаходитись ваш репозиторій у git, потім склонувати репозиторій з GitHub командою<br>
git clone <посилання на репозиторій><br>

2. Додати до файлу package.json залежності у розділи "dependencies" та "devDependencies".<br>

Після виконання цих кроків вводимо команду npm install у тому ж вікні, де клонували репозиторій, вводимо команду у кореневому репозиторії, де лежить package.json<br><br>

### npm start
Команда використовується, щоб запустити головну програму (сервер) проєкту Node.js.<br>

### Що робить
Виконує команду node server.js (запускає файл server.js)<br>

### Коли виконувати
Після того, як ви вже зробили npm install.<br>
1. Коли хочете запустити сервер, щоб перевірити, як працюють маршрути.<br>
2. Коли тестуєте API у Postman або браузері.<br>

### Куди вводити
Команду вводити у терміналі в кореневій папці проєкту (там, де лежить package.json).<br>
Якщо сервер налаштований правильно, після цього у терміналі з’явиться повідомлення на кшталт:<br>
> Server running on http://localhost:3000

### npm test
Використовується, щоб запустити тести або перевірку роботи програми.<br>

### Що робить
Виконує команду node test-client.js.<br> 
Запускає файл test-client.js, який автоматично надсилає запити до сервера (GET, POST, DELETE),<br>
перевіряє, як він відповідає, виводить у консоль результати тестів (наприклад, статуси 200, 401 тощо).<br>

### Коли виконувати
Після запуску сервера (npm start), якщо тести звертаються до нього.<br>
Вводимо щоб перевірити, чи ваш сервер правильно обробляє всі запити й повертає потрібні статуси.

### Куди вводити
У кореневій папці проєкту<br><br><br>


## Таблиця реалізованих ендпоінтів <br>

| HTTP-метод | URL | Опис ендпоінту | Необхідні заголовки для аутентифікації | Приклад тіла запиту (JSON) | Можливі коди відповіді |
|-------------|-----|----------------|----------------------------------------|-----------------------------|-------------------------|
| **GET** | `/documents` | Отримати список усіх документів, доступних користувачу | `X-Login: user1`<br>`X-Password: password123` | – | **200 OK** – успішне отримання списку<br>**401 Unauthorized** – відсутні або неправильні дані авторизації |
| **GET** | `/documents/id` | Отримати конкретний документ за його ID | `X-Login: user1`<br>`X-Password: password123` | – | **200 OK** – документ знайдено<br>**404 Not Found** – документа з таким ID немає<br>**401 Unauthorized** – помилка авторизації |
| **POST** | `/documents` | Створити новий документ | `X-Login: admin1` або `user1`<br>`X-Password: password123` | ```json<br>{<br>  "title": "New Document",<br>  "content": "Some content text"<br>}``` | **201 Created** – документ створено<br>**400 Bad Request** – відсутні або некоректні поля<br>**401 Unauthorized** – невірні дані авторизації |
| **DELETE** | `/documents/id` | Видалити документ за ID (доступно лише адміну) | `X-Login: admin1`<br>`X-Password: password123` | – | **204 No Content** – документ успішно видалено<br>**404 Not Found** – документ не знайдено<br>**401 Unauthorized** – невірні облікові дані<br>**403 Forbidden** – користувач не має прав доступу |
| **GET** | `/employees` | Отримати список співробітників (лише для адміністратора) | `X-Login: admin1`<br>`X-Password: password123` | – | **200 OK** – список отримано<br>**401 Unauthorized** – неавторизований доступ<br>**403 Forbidden** – користувач не є адміністратором |

<br><br>
## Демонстрування успішності основних сценаріїв у Postman
### 1) GET  /documents  401 Unauthorized<br>
<img width="939" height="377" alt="Пункт 5 проверка 2 (1)" src="https://github.com/user-attachments/assets/7bb25864-3a25-4e85-9190-3ae9437cbaaa" /><br><br>
### 2) GET  /employees  403 Forbidden<br>
<img width="937" height="382" alt="Пункт 5 проверка 2 (2)" src="https://github.com/user-attachments/assets/8b161552-82b7-4b8f-aef3-44af7f475645" /><br><br>
### 3) GET  /documents  200 OK<br>
<img width="941" height="375" alt="Пункт 5 проверка 2 (3)" src="https://github.com/user-attachments/assets/111ab484-bf47-47bf-9061-b86d4f166868" /><br><br>
### 4) GET  /employees  200 OK<br>
<img width="946" height="543" alt="Пункт 5 проверка 2 (4)" src="https://github.com/user-attachments/assets/cfee3adf-75c1-4dc6-a329-f6f3f1401b17" /><br><br>
### 5) POST /documents  201 Created<br>
<img width="949" height="414" alt="Пункт 5 проверка 2 (5)" src="https://github.com/user-attachments/assets/892639b6-209a-45db-b2ec-24f8e2775775" /><br><br>
### 6) POST /documents  400 Bad Request<br>
<img width="937" height="370" alt="Пункт 5 проверка 2 (6)" src="https://github.com/user-attachments/assets/8b12b819-f511-4cc3-96f3-0b43796816f2" /><br><br>
### 7) DELETE /documents/1  204 No Content<br>
<img width="950" height="342" alt="Пункт 5 проверка 2 (7)" src="https://github.com/user-attachments/assets/18816c6f-bd28-41a8-978f-9959c3938711" /><br><br>
### 8) GET /non-existent  404 Not Found<br>
<img width="938" height="558" alt="Пункт 5 проверка 2 (8)" src="https://github.com/user-attachments/assets/16fb395d-367e-421b-bcd9-be668534d57e" /><br><br>






