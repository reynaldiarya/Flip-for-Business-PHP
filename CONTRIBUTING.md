# Contributing to Flip for Business PHP

## Introduction

Contributions to this unofficial Flip for Business PHP client are welcome. The goal of contributions is to improve the library's functionality, add support for unimplemented Flip APIs (Disbursement, Virtual Account), fix bugs, enhance documentation, and maintain code quality. All contributions that align with the project's scope and coding standards will be reviewed.

## Getting Started

### Prerequisites
- PHP 8.1 or higher
- Composer

### Local Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/Akselerasi-Prima-Digital/Flip-for-Business-PHP.git
   cd Flip-for-Business-PHP
   ```
2. Install dependencies:
   ```bash
   composer install
   ```

## Development Workflow

### Branch Naming
Use the following prefixes for branches:
- `feature/` for new features or API integrations
- `fix/` for bug fixes
- `docs/` for documentation updates
- `chore/` for maintenance tasks (dependency updates, tooling changes)

### Create a Branch
```bash
git checkout -b feature/add-disbursement-api
```

## Coding Standards

- Follow the existing codebase style, including strict type declarations (`declare(strict_types=1)`) and PSR-4 autoloading conventions.
- Adhere to PSR-12 coding standards, enforced by PHP-CS-Fixer (included in require-dev dependencies).
- Run PHP-CS-Fixer before committing changes to ensure consistent formatting:
  ```bash
  ./vendor/bin/php-cs-fixer fix
  ```
- Maintain clear, descriptive naming for classes, methods, and variables.
- New API client classes should follow the structure of the existing `AcceptPayment` module.

## Commit Guidelines

Use [Conventional Commits](https://www.conventionalcommits.org/) format for commit messages to keep history readable. Examples:
```
feat: add Disbursement API client
fix: handle invalid JSON response in AcceptPayment request
docs: update CreateBill example with required fields
chore: update phpunit to 12.5.24
```

Keep commits focused on a single logical change. Avoid bundling unrelated modifications in one commit.

## Pull Request Process

1. Fork the repository and push your branch to your fork.
2. Open a Pull Request (PR) to the `main` branch of the original repository.
3. Include a clear PR description with:
   - Summary of changes
   - Purpose of the modification
   - Links to related GitHub Issues (if applicable)
4. Ensure all existing tests pass and add new tests for new functionality.
5. PR titles should follow Conventional Commits format.

## Testing

- Run the full test suite with:
  ```bash
  ./vendor/bin/phpunit
  ```
- Integration tests require a valid Flip for Business sandbox API key. If no key is configured, integration tests will be skipped automatically.
- Add PHPUnit tests for all new features or bug fixes, following the structure of existing test files in the tests directory.

## Issue Reporting

Use GitHub Issues for bug reports and feature requests:
- **Bug reports**: Include steps to reproduce, expected behavior, actual behavior, PHP version, library version, and Flip environment (sandbox/production).
- **Feature requests**: Explain the use case, expected functionality, and reference official Flip API documentation if proposing new API integrations.

## Security

Do not report security vulnerabilities via public GitHub Issues. Contact the maintainers privately via email at info@akseprima.com with details of the vulnerability, steps to reproduce, and potential impact.

## Code of Conduct

All contributors are expected to communicate respectfully and professionally. Focus on constructive feedback, avoid discriminatory or harassing language, and prioritize collaborative problem-solving.

## Additional Notes

- This is an unofficial client for Flip for Business APIs. Ensure new API integrations match the official Flip API documentation.
- Maintain backward compatibility for minor and patch releases. Breaking changes require a major version bump.
- The static `Config` class is used for global configuration; avoid introducing instance-level configuration changes without prior discussion.
- Unimplemented APIs referenced in the project description (Disbursement, Virtual Account) should follow the same pattern as the `AcceptPayment` module when contributed.