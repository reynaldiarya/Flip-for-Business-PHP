# Flip for Business PHP

A PHP client library for integrating Flip for Business payment APIs into applications, enabling programmatic access to Accept Payment, disbursement, and virtual account services.

<p align="center">
  <img src="https://img.shields.io/badge/version-0.0.1-blue" />
  <img src="https://img.shields.io/badge/PHP-8.1+-777BB4" />
  <a href="LICENSE">
    <img alt="License" src="https://img.shields.io/badge/license-MIT-yellow" target="_blank" />
  </a>
</p>

## Description

Flip for Business PHP provides a structured interface to interact with Flip's payment infrastructure through HTTP API calls. The library handles authentication, request formatting, and response parsing, allowing developers to integrate payment collection, bill management, and transaction tracking without building raw HTTP implementations.

The client targets businesses and developers building payment flows that require bill creation, payment status retrieval, and transaction management through Flip's platform. It supports both sandbox and production environments with minimal configuration changes.

## Features

- **Accept Payment API Integration** - Create and manage payment bills with support for single and multiple payment types
- **Bill Lifecycle Management** - Create, retrieve, edit, and list bills through dedicated methods
- **Payment Tracking** - Query individual payments or retrieve filtered payment lists
- **Environment Configuration** - Switch between sandbox and production endpoints via a single flag
- **Debug Logging** - Optional request and response logging for development and troubleshooting
- **Exception Handling** - Structured error handling with custom FlipException and HttpException classes
- **Webhook Verification** - Built-in support for HMAC webhook secret configuration
- **Guzzle HTTP Client** - Powered by Guzzle with configurable headers and middleware support

## Tech Stack

- **Language**: PHP 8.1+
- **HTTP Client**: Guzzle HTTP 7.10.0
- **Testing**: PHPUnit 12.5.24
- **Code Standards**: PHP-CS-Fixer
- **Namespace**: `AkselerasiPrimaDigital\FlipForBusinessPhp`

## Installation

### Prerequisites

- PHP 8.1 or higher
- Composer

### Steps

1. Install via Composer

```bash
composer require akselerasiprimadigital/flip-for-business-php
```

2. Or clone and install manually

```bash
git clone https://github.com/Akselerasi-Prima-Digital/Flip-for-Business-PHP.git
cd Flip-for-Business-PHP
composer install
```

## Configuration

The library uses a static `Config` class for configuration. Set the following properties before initializing the client:

### API Credentials

| Property | Type | Description |
|----------|------|-------------|
| `Config::$apiKey` | string | Your Flip for Business API key |
| `Config::$webhookSecret` | string | Secret key for verifying webhook HMAC signatures |
| `Config::$isProduction` | bool | Set to `true` for production, `false` for sandbox (default) |
| `Config::$debug` | bool | Enable request/response logging via `error_log` |

### Environment Endpoints

The library automatically selects the correct base URL based on the environment setting:

- **Sandbox**: `https://bigflip.id/big_sandbox_api/v2`
- **Production**: `https://bigflip.id/api/v2`

```php
use AkselerasiPrimaDigital\FlipForBusinessPhp\Config;

// Set API key
Config::$apiKey = 'your-api-key-here';

// Use sandbox environment
Config::$isProduction = false;

// Enable debug logging (optional)
Config::$debug = true;
```

## Usage

### Initializing the Client

```php
require 'vendor/autoload.php';

use AkselerasiPrimaDigital\FlipForBusinessPhp\Config;
use AkselerasiPrimaDigital\FlipForBusinessPhp\FlipForBusiness;

// Configure
Config::$apiKey = 'YOUR_API_KEY';
Config::$isProduction = false; // or true for production

// Initialize client
$flip = new FlipForBusiness();
```

### Accept Payment - Create Bill

```php
try {
    $bill = $flip->acceptPayment()->createBill([
        'title' => 'Coffee Table',
        'type' => 'SINGLE',
        'amount' => 900000,
        'expired_date' => '2025-12-30 15:50',
        'redirect_url' => 'https://your-site.com/return',
        'step' => 'direct_api'
    ]);

    print_r($bill);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

### Accept Payment - Get Bill by ID

```php
try {
    $bill = $flip->acceptPayment()->getBill('bill-id-here');
    print_r($bill);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

### Accept Payment - List All Bills

```php
try {
    $bills = $flip->acceptPayment()->getAllBill();
    print_r($bills);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

### Accept Payment - Edit Bill

```php
try {
    $updated = $flip->acceptPayment()->editBill('bill-id-here', [
        'title' => 'Updated Title',
        'amount' => 950000
    ]);
    print_r($updated);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

### Accept Payment - Get Payment Details

```php
try {
    $payment = $flip->acceptPayment()->getPayment('bill-id-here');
    print_r($payment);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

### Accept Payment - List Payments with Filters

```php
try {
    $payments = $flip->acceptPayment()->getAllPayment([
        'limit' => 10,
        'status' => 'PAID'
    ]);
    print_r($payments);
} catch (\Throwable $e) {
    echo $e->getMessage();
}
```

## Project Structure

```
src/
├── Config.php                      # Static configuration class
├── FlipForBusiness.php             # Main client class and HTTP initialization
├── AcceptPayment/
│   └── AcceptPayment.php           # Accept Payment API methods
└── Exceptions/
    ├── FlipException.php           # Custom exception for API errors
    └── HttpException.php           # HTTP-level exception wrapper

examples/
└── AcceptPayment/
    ├── CreateBill.php              # Example: creating a bill
    ├── EditBill.php                # Example: editing a bill
    ├── GetAllBill.php              # Example: listing all bills
    ├── GetAllPayment.php           # Example: listing payments
    ├── GetBill.php                 # Example: retrieving a bill
    └── getPayment.php              # Example: retrieving payment details

tests/
└── AcceptPaymentTest.php           # PHPUnit integration tests
```

## Scripts / Commands

### Composer Scripts

| Command | Description |
|---------|-------------|
| `composer install` | Install PHP dependencies |
| `composer update` | Update PHP dependencies |
| `composer require akselerasiprimadigital/flip-for-business-php` | Install the package |

### Testing

```bash
# Run all tests
./vendor/bin/phpunit

# Run with configuration
./vendor/bin/phpunit -c phpunit.xml.dist
```

### Code Style

```bash
# Run PHP-CS-Fixer (if configured)
./vendor/bin/php-cs-fixer fix
```

## Contributing

Contributions are welcome. To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow PSR-12 coding standards
- Write tests for new features using PHPUnit
- Ensure compatibility with PHP 8.1+
- Update examples when adding new API methods
- Document new configuration options in the Config class

## License

This project is open-sourced software licensed under the MIT License.

## Author

Akselerasi Prima Digital