# Інструкція для запуску контейнера MySQL та програми

## 1. Запуск контейнера MySQL

Щоб запустити контейнер з MySQL, виконайте наступні кроки:

1. **Побудуйте образ MySQL** з Dockerfile, якщо ви ще не зробили цього:

    ```bash
    docker build -t salo2452/mysql-local:1.0.0 .
    ```

2. **Запустіть контейнер MySQL** з приєднаним томом для зберігання даних:

    ```bash
    docker run -d --name mysql-container -v mysql-data:/var/lib/mysql -p 3306:3306 salo2452/mysql-local:1.0.0
    ```

    - `-d` — працювати в фоновому режимі.
    - `--name mysql-container` — вказуємо ім'я контейнера.
    - `-v mysql-data:/var/lib/mysql` — створюємо том для зберігання даних MySQL.
    - `-p 3306:3306` — відкриваємо порт 3306 для доступу до MySQL з зовнішнього середовища.

## 2. Запуск контейнера програми

1. Оновіть конфігурацію вашої програми для підключення до контейнера MySQL. Використовуйте IP-адресу контейнера MySQL для підключення. Ви можете дізнатися IP-адресу контейнера за допомогою наступної команди:

    ```bash
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mysql-container
    ```

2. **Побудуйте образ програми**:

    ```bash
    docker build -t salo2452/todoapp:2.0.0 .
    ```

3. **Запустіть контейнер програми** та підключіть його до контейнера MySQL:

    ```bash
    docker run -d --name todoapp-container --link mysql-container:mysql -p 8000:8000 salo2452/todoapp:2.0.0
    ```

    - `--link mysql-container:mysql` — дозволяє контейнеру програми підключатися до контейнера MySQL.
    - `-p 8000:8000` — відкриває порт 8000 для доступу до програми через браузер.

## 3. Доступ до програми через браузер

Щоб отримати доступ до вашої програми, відкрийте браузер і перейдіть за адресою:


## 4. Ваші образи на Docker Hub

- **MySQL образ**: [salo2452/mysql-local:1.0.0](https://hub.docker.com/r/salo2452/mysql-local)
- **Програма**: [salo2452/todoapp:2.0.0](https://hub.docker.com/r/salo2452/todoapp)

## 5. Створення PR

1. Створіть Pull Request з вашими змінами на платформі для перевірки.

