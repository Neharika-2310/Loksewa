# 🏛️ Loksewa — Civil Service Exam Preparation Platform

## 📖 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [Artisan Commands Reference](#artisan-commands-reference)
- [Frontend Development](#frontend-development)
- [Authentication](#authentication)
- [Database](#database)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## 📌 About the Project

**Loksewa** is a web-based platform built to assist aspirants preparing for Nepal's **Lok Sewa Aayog (Public Service Commission)** examinations. The application provides a structured, user-friendly environment for exam practice, study materials, and progress tracking.

Built on **Laravel 11** with **Bootstrap 5** for a responsive, modern UI, and secured with **Laravel Breeze** authentication — Loksewa is designed for scalability, performance, and ease of use.

---

## ✨ Features

- 🔐 **User Authentication** — Secure registration, login, logout, and password reset via Laravel Breeze
- 📊 **User Dashboard** — Personalized dashboard for authenticated users
- 📝 **Exam Practice** — (Extendable) Question banks and mock test modules
- 📱 **Responsive UI** — Fully mobile-friendly using Bootstrap 5
- ⚡ **Fast Frontend** — Asset bundling with Vite for optimized builds
- 🌐 **Nepali Timezone Support** — Configured for `Asia/Kathmandu`
- 🛡️ **CSRF Protection** — Laravel's built-in security middleware

---

## 🛠️ Tech Stack

| Layer         | Technology                          |
|---------------|-------------------------------------|
| Backend       | PHP 8.2+, Laravel 11                |
| Frontend      | Bootstrap 5.3, Alpine.js 3.x        |
| Templating    | Blade                               |
| Build Tool    | Vite 6.x                            |
| Database      | MySQL 5.7+                          |
| Auth          | Laravel Breeze                      |
| Package Mgr   | Composer 2.x, npm 11.x              |
| Dev Server    | PHP built-in / Laravel Artisan      |

---

## 📁 Project Structure

```
loksewa/
├── app/
│   ├── Http/
│   │   ├── Controllers/        # Application controllers
│   │   └── Middleware/         # HTTP middleware
│   ├── Models/                 # Eloquent models
│   └── Providers/              # Service providers
├── bootstrap/                  # Framework bootstrap files
├── config/                     # Application configuration files
├── database/
│   ├── factories/              # Model factories for testing
│   ├── migrations/             # Database schema migrations
│   └── seeders/                # Database seeders
├── public/
│   ├── build/                  # Compiled frontend assets (Vite output)
│   └── index.php               # Application entry point
├── resources/
│   ├── css/                    # Source CSS (Bootstrap imports)
│   ├── js/                     # Source JavaScript (Alpine.js, etc.)
│   └── views/                  # Blade templates & components
├── routes/
│   ├── web.php                 # Web routes
│   ├── api.php                 # API routes
│   └── auth.php                # Authentication routes (Breeze)
├── storage/                    # Logs, file uploads, cache
├── tests/                      # Feature and unit tests
├── .env.example                # Environment variable template
├── artisan                     # Laravel CLI entry point
├── composer.json               # PHP dependency manifest
├── package.json                # Node.js dependency manifest
├── tailwind.config.js          # Tailwind config (retained)
└── vite.config.js              # Vite bundler configuration
```

---

## ✅ Prerequisites

Make sure you have the following installed before setting up the project:

- **PHP** >= 8.2 with extensions: `OpenSSL`, `PDO`, `Mbstring`, `Fileinfo`, `BCMath`, `Ctype`, `JSON`, `Tokenizer`, `XML`
- **Composer** >= 2.x
- **Node.js** >= 18.x and **npm** >= 9.x
- **MySQL** >= 5.7 (or MariaDB 10.4+)
- **XAMPP / WAMP / Laragon** (for local development) or any web server stack

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Neharika-2310/Loksewa.git
cd Loksewa
```

### 2. Install PHP Dependencies

```bash
composer install
```

> If Composer is not globally installed, use the bundled `composer.phar`:
> ```bash
> php composer.phar install
> ```

### 3. Install Node.js Dependencies

```bash
npm install
```

### 4. Set Up Environment Variables

```bash
cp .env.example .env
php artisan key:generate
```

Then configure your `.env` file (see [Environment Configuration](#environment-configuration) below).

### 5. Create the Database

Create a MySQL database named `loksewa` using phpMyAdmin, MySQL CLI, or your preferred tool:

```sql
CREATE DATABASE loksewa CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 6. Run Database Migrations

```bash
php artisan migrate
```

This creates the following tables:

- `users`
- `password_reset_tokens`
- `sessions`
- `cache`
- `jobs`
- `failed_jobs`

### 7. Build Frontend Assets

```bash
npm run build
```

---

## ⚙️ Environment Configuration

Edit your `.env` file with the following key settings:

```dotenv
APP_NAME=Loksewa
APP_ENV=local
APP_KEY=base64:...          # Auto-generated by artisan key:generate
APP_DEBUG=true
APP_URL=http://localhost:8000
APP_TIMEZONE=Asia/Kathmandu

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=loksewa
DB_USERNAME=root
DB_PASSWORD=                 # Leave empty for XAMPP default; set if your MySQL has a password

SESSION_DRIVER=file          # Change to 'database' for DB-based sessions
MAIL_MAILER=log              # Change to 'smtp' for real email sending
```

---

## ▶️ Running the Application

### Start the Development Server

```bash
php artisan serve
```

The app will be accessible at: **http://localhost:8000**

### Run Frontend in Watch Mode (Hot Reload)

```bash
npm run dev
```

### Run Both Simultaneously (Recommended)

```bash
composer run dev
```

This runs the server, queue listener, log watcher, and Vite — all concurrently.

---

## 🧰 Artisan Commands Reference

```bash
# Server
php artisan serve                                 # Start development server
php artisan serve --port=8001                     # Use alternate port

# Database
php artisan migrate                               # Run all pending migrations
php artisan migrate:fresh --seed                  # Drop all tables, re-migrate, and seed
php artisan db:seed                               # Run database seeders

# Code Generation
php artisan make:model ModelName -mcr             # Create model, migration, controller
php artisan make:controller ControllerName        # Create a controller
php artisan make:migration create_table_name      # Create a new migration

# Cache Management
php artisan cache:clear                           # Clear application cache
php artisan config:clear                          # Clear config cache
php artisan config:cache                          # Cache config for performance
php artisan view:clear                            # Clear compiled views

# Debugging
php artisan tinker                                # Interactive REPL shell
php artisan route:list                            # List all registered routes
```

---

## 🎨 Frontend Development

The project uses **Vite** as the build tool with **Bootstrap 5** as the CSS framework.

### Key Frontend Files

| File                          | Purpose                                 |
|-------------------------------|-----------------------------------------|
| `resources/css/app.css`       | Main stylesheet (imports Bootstrap)     |
| `resources/js/app.js`         | Main JS (Bootstrap + Alpine.js)         |
| `vite.config.js`              | Vite bundler configuration              |
| `postcss.config.js`           | PostCSS configuration (Autoprefixer)    |
| `public/build/`               | Compiled production assets              |

### Commands

```bash
npm run dev      # Development mode with hot reload
npm run build    # Production build (minified & hashed)
```

---

## 🔐 Authentication

Authentication is powered by **Laravel Breeze** using Blade templates styled with Bootstrap 5.

### Available Auth Routes

| Route                  | Description                    |
|------------------------|--------------------------------|
| `GET /register`        | User registration page         |
| `POST /register`       | Process registration           |
| `GET /login`           | Login page                     |
| `POST /login`          | Process login                  |
| `POST /logout`         | Logout current user            |
| `GET /forgot-password` | Password reset request page    |
| `GET /dashboard`       | Authenticated user dashboard   |

### Create a Test User via Tinker

```bash
php artisan tinker
```

```php
User::create([
    'name'     => 'Test User',
    'email'    => 'test@example.com',
    'password' => Hash::make('password123'),
]);
exit;
```

---

## 🗄️ Database

- **Engine**: MySQL 5.7+ / MariaDB 10.4+
- **Default Database Name**: `loksewa`
- **ORM**: Laravel Eloquent
- **Migrations**: Located in `database/migrations/`

### Useful Database Commands

```bash
php artisan migrate:status          # Check migration status
php artisan migrate:rollback        # Rollback last batch of migrations
```

---

## 🔧 Troubleshooting

### Port 8000 Already in Use

```bash
php artisan serve --port=8001
```

### Clear All Caches

```bash
php artisan cache:clear
php artisan config:clear
php artisan view:clear
php artisan route:clear
```

### Database Connection Issues

1. Ensure MySQL is running (check XAMPP Control Panel)
2. Verify credentials in `.env` match your local MySQL setup
3. Confirm the `loksewa` database exists in phpMyAdmin

### Asset Build Issues

```bash
npm install        # Reinstall node modules
npm run build      # Rebuild production assets
```

### Permission Errors on Storage

```bash
chmod -R 775 storage bootstrap/cache
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m 'feat: add your feature description'`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

Please follow the [PSR-12 PHP coding standard](https://www.php-fig.org/psr/psr-12/) and write tests where applicable.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 👩‍💻 Author

**Neharika** — [@Neharika-2310](https://github.com/Neharika-2310)

---

> **Note:** This project is under active development. Features may change as development progresses.
