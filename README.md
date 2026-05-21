<p align="center"><img src="https://raw.githubusercontent.com/dewanakl/Kamu/main/public/kamu.png" width="200" alt="kamu"></p>

<p align="center">
<a href="https://php.net"><img src="https://img.shields.io/packagist/dependency-v/kamu/framework/php.svg?color=birghtgreen" alt="PHP Programming Language"></a>
<a href="https://packagist.org/packages/kamu/framework"><img src="https://img.shields.io/packagist/dt/kamu/framework" alt="Total Downloads"></a>
<a href="https://cie.my.id"><img src="https://cie.my.id/undangan-api?label=views&color=brightgreen" alt="views"></a>
<a href="https://shields.io"><img src="https://img.shields.io/github/repo-size/dewanakl/undangan-api?color=brightgreen" alt="Repo size"></a>
<a href="https://shields.io"><img src="https://img.shields.io/github/license/dewanakl/undangan-api?color=brightgreen" alt="License"></a>
</p>

## 📖 About Kamu

"Kamu" merupakan PHP framework yang sangat simpel, memberikan pengalaman seolah-olah berada di localhost meskipun dalam mode production. Dibantu dengan "Saya" konsol yang membantu pengembangan aplikasi secara efisien.

## 📡 Api Spec

See in postman collection
```url
https://www.postman.com/dewanakl/workspace/undangan/collection/20716209-a29ef362-b4dc-4c02-8904-d90749a40842?action=share
```

> [!WARNING]
> Gunakan versi 3.7.2, untuk versi 4 masih tahap pengembangan dan berpotensi teredapat bug 🐛

## ☁️ Deployment

<details>
<summary>🛠️ Run without docker</summary>

- Create file env

    ```bash
    cp .env.example .env
    ```

- Install package

    ```bash
    composer install
    ```

- Create key application

    ```bash
    php saya key
    ```

- Execute migration database

    ```bash
    php saya migrasi --gen
    ```

- Setup JWT_KEY in .env file

    ```bash
    JWT_KEY=your_secret_key_here
    ```

- Create admin user (API has no registration endpoint)

    Create a PHP script to insert user into database:

    ```php
    <?php
    $pdo = new PDO('mysql:host=127.0.0.1;port=3306;dbname=kamu', 'root', '');
    $password = password_hash('your_password', PASSWORD_DEFAULT);
    $stmt = $pdo->prepare('INSERT INTO users (name, email, password, created_at, updated_at, is_active) VALUES (?, ?, ?, NOW(), NOW(), 1)');
    $stmt->execute(['Admin Name', 'admin@example.com', $password]);
    echo "User created successfully\n";
    ```

    Or run directly in MySQL:

    ```sql
    INSERT INTO users (name, email, password, created_at, updated_at, is_active)
    VALUES ('Admin Name', 'admin@example.com', '$2y$10$hashed_password_here', NOW(), NOW(), 1);
    ```

- Run in development server

    ```bash
    php saya coba
    ```
</details>

<details>
<summary>🐳 Run with docker</summary>

- Create file env

    ```bash
    cp .env.example .env
    ```

- Change and customize env file

    ```text
    BASEURL=https://your.domain.or.ipaddress:8080/

    DB_DRIV=pgsql
    DB_HOST=db
    DB_PORT=5432
    DB_NAME=undangan
    DB_USER=root
    DB_PASS=12345678

    JWT_KEY=valueIsSecure
    ```

- Build and run image

    ```bash
    docker compose up --build -d
    ```

- Execute migration

    > **_NOTE:_** Wait until the database is ready.

    ```bash
    docker exec undangan-app php saya migrasi --gen
    ```
</details>

<details>
<summary>⚡ Deployment on vercel</summary>

- Create .env file

    ```bash
    cp .env.example .env
    ```

- Install package

    ```bash
    composer install
    ```

- Create key application

    ```bash
    php saya key
    ```

- Execute migration database

    ```bash
    php saya migrasi --gen
    ```

- Push on your github.
- Create new project in vercel.
- Import from your repository.
- Add environment variables :
  - DB_HOST (your host cloud dbms)
  - DB_PASS (your password cloud dbms)
  - DB_USER (your username cloud dbms)
  - DB_NAME (your name of database cloud dbms)
  - DB_PORT (your port cloud dbms)
  - DB_DRIV (type cloud dbms [ex. mysql or pgsql])
  - JWT_KEY [ex. 123]
  - HTTPS [true]
  - DEBUG [false]
  - LOG [false]
  - APP_KEY [copy from your local env]
- Done.
</details>

## 🚀 Get Started Project

- Create a project with composer

    ```bash
    composer create-project kamu/kamu coba-app
    ```

- Move the folder

    ```bash
    cd coba-app
    ```

- Run in development server

    ```bash
    php saya coba
    ```

## 🤝 Contributing

I'm very open to those of you who want to contribute to Kamu framework!

## 🐞 Security Vulnerabilities

If you find a security vulnerability in this Kamu, please email DKL via [dewanakretarta29@gmail.com](mailto:dewanakretarta29@gmail.com).

## 📜 License

Kamu framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
