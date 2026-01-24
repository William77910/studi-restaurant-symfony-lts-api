# STUDI Restaurant API - Development Environment Setup

## Quick Try (Docker)

```bash
cp .env.example .env.local
docker-compose up -d
docker-compose exec php php bin/console doctrine:database:create
docker-compose exec php php bin/console doctrine:migrations:migrate
docker-compose exec php php bin/console doctrine:fixtures:load --no-interaction
```

Access: http://localhost:8000/api/doc

---

## Quick Try (Local)

```bash
composer install
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
php bin/console doctrine:fixtures:load --no-interaction
symfony server:start
```

Access: http://127.0.0.1:8000/api/doc

---

Tip (Composer): lock platform to avoid conflicts

```bash
composer config platform.php 8.1
composer install
```

---

Windows Tip (Global Composer config)

- Config file path: `C:\Users\<YOU>\AppData\Roaming\Composer\config.json`
- Ensure:

```json
{
  "config": { "secure-http": true }
}
```

- Remove `disable-tls` if present.
- Verify:

```powershell
composer config --global --list | Select-String -Pattern "secure-http|disable-tls"
```

---

macOS/Linux Tip (Global Composer config)

- Config file path: `~/.composer/config.json`
- Ensure:

```json
{
  "config": { "secure-http": true }
}
```

- Remove `disable-tls` if present.
- Verify:

```bash
composer config --global --list | grep -E "secure-http|disable-tls"
```

---

## Quick Start (Recommended: Docker)

### Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

### Setup with Docker

1. **Clone and setup:**

```bash
git clone git@github.com:GaetanRole/studi-restaurant-symfony-lts-api.git
cd studi-restaurant-symfony-lts-api
cp .env.example .env.local
```

2. **Start containers:**

```bash
docker-compose up -d
```

3. **Initialize database:**

```bash
docker-compose exec php php bin/console doctrine:database:create
docker-compose exec php php bin/console doctrine:migrations:migrate
docker-compose exec php php bin/console doctrine:fixtures:load --no-interaction
```

4. **Access the application:**

- API: http://localhost:8000
- API Documentation: http://localhost:8000/api/doc
- Database (MySQL): localhost:3306 (user: restaurant_user, password: restaurant_password)

5. **Useful Docker commands:**

```bash
# Stop containers
docker-compose down

# View logs
docker-compose logs -f php

# Execute commands
docker-compose exec php php bin/console debug:router
docker-compose exec php php bin/console cache:clear

# Access database
docker-compose exec db mysql -urestaurant_user -p restaurant_db
```

---

## Alternative: Local Setup (XAMPP/Native PHP)

### Prerequisites

- PHP >= 8.1
- MySQL >= 8.0
- Composer
- Symfony CLI

### Installation

1. **Clone repository:**

```bash
git clone git@github.com:GaetanRole/studi-restaurant-symfony-lts-api.git
cd studi-restaurant-symfony-lts-api
```

2. **Copy environment file:**

```bash
cp .env .env.local
```

Edit `.env.local` with your local database credentials.

3. **Install dependencies:**

```bash
composer install
```

4. **Setup database:**

```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
php bin/console doctrine:fixtures:load --no-interaction
```

5. **Start development server:**

```bash
symfony server:start
```

6. **Access the application:**

- API: http://127.0.0.1:8000
- API Documentation: http://127.0.0.1:8000/api/doc

---

## Environment Compatibility

This project is configured for PHP 8.1 (LTS) with Symfony 5.4 (LTS) to ensure stability.

### Verify your environment:

```bash
# For Docker
docker-compose exec php php -v
docker-compose exec php php -m | grep -E "curl|pdo|pdo_mysql|json"

# For local setup
php -v
php -m | grep -E "curl|pdo|pdo_mysql|json"
```

### Composer platform lock

The project uses `composer config platform.php 8.1` to ensure all developers resolve dependencies against PHP 8.1, regardless of their local PHP version. This prevents "works on my machine" issues.

---

## Documentation

- [Symfony Documentation](https://symfony.com/doc/5.4)
- [API Documentation](http://localhost:8000/api/doc)
- [Nelmio API Doc](https://github.com/nelmio/NelmioApiDocBundle)
- [OpenAPI/Swagger PHP](https://github.com/zircote/swagger-php)

---

## OpenAPI (Swagger + Nelmio)

- For swagger-php ≥ 5.x use attributes:

```php
use OpenApi\Attributes as OA;
```

- Prefer PHP 8 attributes over legacy DocBlocks:

```php
#[OA\Get(path: '/api/restaurant/{id}')]
```

- Refresh documentation when changing annotations:

```bash
php bin/console cache:clear
```

---

## Project Checklist (for new setups)

- Identify target versions (PHP/Symfony/libs)
- `composer config platform.php 8.1`
- Copy `docker-compose.yml` if using Docker
- Configure `.env.local` (DATABASE_URL, etc.)
- `composer install` then run migrations & fixtures
- Test `/api/doc` and key routes

---

## Troubleshooting

### Docker won't start

```bash
docker-compose down
docker system prune -a
docker-compose up -d --build
```

### Database connection error

- Verify `DATABASE_URL` in `.env.local`
- Check MySQL container: `docker-compose logs db`
- Ensure database exists: `docker-compose exec php php bin/console doctrine:database:create`

### Composer dependency conflicts

The project uses `"platform": { "php": "8.1" }` in `composer.json` to lock dependency resolution. If you see conflicts:

```bash
composer install --prefer-dist
```

### Composer TLS/SSL disabled

- Global Composer config file on Windows: `C:\Users\<you>\AppData\Roaming\Composer\config.json`
- Ensure:

```json
{
  "config": { "secure-http": true }
}
```

- Remove `disable-tls` if present.

### Docker containers won't start or are unstable

```bash
docker-compose down
docker system prune -a
docker-compose up -d --build
```

### Clear cache after changes

```bash
php bin/console cache:clear
# or with Docker:
docker-compose exec php php bin/console cache:clear
```

---

## Contributing

Follow the project structure and style conventions. No external contributions allowed (STUDI proprietary).

---

## License

Proprietary - STUDI exclusive.

---

## Best Practices

- Lock Composer platform early (PHP 8.1)
- Prefer Docker for consistent environments
- Clear Symfony cache after structural changes
- Upgrade versions gradually and read CHANGELOGs

---

Last updated: January 24, 2026

[⬆️ Back to top](#studi-restaurant-api---development-environment-setup)
