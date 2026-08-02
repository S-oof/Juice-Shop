# Juice-Shop
OWASP Juice Shop — це один із найкращих сучасних інструментів для вивчення веб-безпеки. Це навмисно вразливий додаток, написаний на Node.js, Express та Angular. Оскільки він містить понад 100 челенджів, цей посібник допоможе вам пройти перші ключові етапи та зрозуміти логіку гри.

####
Виконайте команду в терміналі: docker run --rm -p 3000:3000 bkimminich/juice-shop. Маємо наступний результат:
<img width="949" height="417" alt="image" src="https://github.com/user-attachments/assets/7ece0bcb-232c-4601-a4ad-2224077192de" />

Відкрийте браузер за адресою: http://localhost:3000
<img width="1919" height="891" alt="image" src="https://github.com/user-attachments/assets/0249caf1-36a4-4b11-bd11-76e0a0733b37" />

Спробуємо власноруч підібрати посилання для проходження першого завдання: до адреси сайту допишемо scoreboard або score-board та перевіримо, чи зможемо ми знайти потрібну сторінку:
<img width="1898" height="743" alt="image" src="https://github.com/user-attachments/assets/c181df16-d87f-41a1-8aa1-fe25d08017e6" />

#### Атака на пошуковий рядок (DOM XSS)
<img width="471" height="227" alt="image" src="https://github.com/user-attachments/assets/2e8f1a22-889e-49f5-8168-b088189220af" />

У полі пошуку (Search) вгорі сторінки введіть скрипт: <iframe src="javascript:alert('xss')">
<img width="1177" height="147" alt="image" src="https://github.com/user-attachments/assets/1f1bc497-f340-4c76-b295-0468defe2be9" />

Має з'явитися вікно з повідомленням, після чого челендж буде зараховано.
<img width="1627" height="482" alt="image" src="https://github.com/user-attachments/assets/b5132ba9-b608-4495-a9c8-bb967aef1caa" />

За таким самим принципом виконання додатково робимо відправку пейлоада:
<img width="1765" height="559" alt="image" src="https://github.com/user-attachments/assets/23bc9da8-57c9-414b-9e0e-6cd79d6f06ca" />

#### Витік конфіденційних даних (Sensitive Data Exposure)
1. Для виконання цього завдання потрібно знайти файл, який не має бути публічним. Спочатку шукаємо відкриті директорії, але отримуємо помилку з довжиною 9903:
<img width="988" height="327" alt="image" src="https://github.com/user-attachments/assets/2e257fbb-5ed7-4693-8ec7-2138ad16b522" />

2. Вносимо зміни, які нам рекомендовано, та знову запускаємо сканування:
<img width="1052" height="490" alt="image" src="https://github.com/user-attachments/assets/25ef4ef5-ab07-4396-8929-c8822e9c7125" />

3. Перезавантажуємо контейнер та вводимо у пошук http://localhost:3000/fpt
<img width="1465" height="454" alt="image" src="https://github.com/user-attachments/assets/5e6a5044-3b8b-435f-84af-87ab6f7c16d7" />

4. Переходимо на файл, який сервер намагається блокувати. Використовуючи обхід фільтрів, завантажимо цей файл (у пошуковий рядок до назви додамо %2500.md). Файл завантажився:
<img width="872" height="700" alt="image" src="https://github.com/user-attachments/assets/6477f9e4-6063-40b6-aecc-755ac53c26aa" />
5. Завдання успішно виконано:
<img width="1893" height="756" alt="image" src="https://github.com/user-attachments/assets/71d69fdf-a806-48dc-859c-d9b9a917870b" />

#### Злам акаунтів
Спочатку перейдемо на сторінку login, у поле емейлу введемо ' OR '1'='1'--. Вводимо будь-який пароль. Вигляд має бути таким:
<img width="661" height="681" alt="image" src="https://github.com/user-attachments/assets/4dc0336c-a26c-4e5a-bddf-308539285f72" />

SQL-ін'єкція успішно спрацювала, ми зайшли до системи як адміністратор:
<img width="413" height="369" alt="image" src="https://github.com/user-attachments/assets/658cc0d5-dd0a-4ccb-b3bc-ae7ae6768757" />



#### Завдання на вибір
#### Broken Access Control (Easter egg)

Для виконання цього завдання спочатку потрібно виконати пункти 1-3 з блоку "Витік конфіденційних даних" (див. вище).
<img width="1514" height="245" alt="image" src="https://github.com/user-attachments/assets/e81d1f46-b62f-4bdb-9a86-ff81cc7adc9e" />
Переходимо на файл під назвою eastere.gg , який сервер намагається блокувати. Використовуючи обхід фільтрів, завантажимо цей файл (у пошуковий рядок до назви додамо %2500.md):
<img width="846" height="567" alt="image" src="https://github.com/user-attachments/assets/02e4a4ee-7e17-4993-be50-64b729f4b84a" />
Файл завантажився. Прочитавши вміст файлу, можемо помітити рядок з набором літер, цифр та спец. символів. Скопіюємо його:
<img width="813" height="618" alt="image" src="https://github.com/user-attachments/assets/c717093b-0b74-4fff-986d-6b4809afcc3e" />
Повернемось на сторінку Juice Shop та вставимо цю частину у пошуковий рядок:
<img width="1149" height="219" alt="image" src="https://github.com/user-attachments/assets/64bea8e4-5948-4851-90d1-0539667ef387" />
Завдання успішно виконано.
<img width="503" height="163" alt="image" src="https://github.com/user-attachments/assets/3e79f5a5-cbe7-4015-b21f-7c7701d16625" />
<img width="1871" height="231" alt="image" src="https://github.com/user-attachments/assets/6602b7b5-3f9a-4fba-b4eb-d1633bf8ecbf" />



