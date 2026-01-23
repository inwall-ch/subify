[![CI Pipeline](https://github.com/web-inwall/subify/actions/workflows/ci.yml/badge.svg)](https://github.com/web-inwall/subify/actions)
[![PHP Version](https://img.shields.io/badge/PHP-8.4-4169E1.svg?style=flat&logo=php&logoColor=white)](https://php.net)
[![Laravel](https://img.shields.io/badge/Laravel-12.x-4169E1.svg?style=flat&logo=laravel&logoColor=white)](https://laravel.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1.svg?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7.x-4169E1.svg?style=flat&logo=redis&logoColor=white)](https://redis.io/)
[![Code Style](https://img.shields.io/badge/code%20style-PSR--12-4169E1)](https://www.php-fig.org/psr/psr-12/)
[![Larastan](https://img.shields.io/badge/Larastan-Level%205-4169E1)](https://github.com/larastan/larastan)

# Subify - SaaS Subscription Management API

A robust, high-performance SaaS subscription management API built for scalability and flexibility.

## 🛠 Tech Stack

- **Framework**: Laravel 12
- **Database**: PostgreSQL
- **Cache & Queues**: Redis
- **Architecture**: Modular Monolith with DDD principles

## ✨ Key Features

- **Pipeline Pattern**: robust and extensible subscription processing workflows.
- **Strategy Pattern**: seamless interchangeability of payment providers.
- **JSONB Optimization**: high-performance storage for dynamic subscription metadata.

## 🚀 Installation

```bash
composer install
cp .env.example .env
php artisan sail:install
./vendor/bin/sail up -d
./vendor/bin/sail artisan migrate
```

## 📖 Architecture
```bash
SubscriptionController → SubscriptionData DTO → SubscribeUserAction → Pipeline:
  ├── EnsurePlanIsAvailable
  ├── ProcessPayment (Strategy)
  └── CreateSubscriptionRecord
```

## 🔌 API Example

### Create a Subscription

**Endpoint**
`POST /api/subscriptions`

**Request**
```json
{
    "user_id": 1,
    "plan": "premium_yearly",
    "payment_gateway": "stripe",
    "options": {
        "tax_id": "US123456789",
        "coupon": "LAUNCH2026"
    }
}
```

**Response**
```json
{
    "data": {
        "id": "sub_01HM8X...",
        "status": "active",
        "starts_at": "2026-01-21T10:00:00Z",
        "renews_at": "2027-01-21T10:00:00Z"
    }
}
```
