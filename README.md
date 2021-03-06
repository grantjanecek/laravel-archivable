# Laravel Archivable

<p align="center">
<a href="https://github.com/joelbutcher/laravel-archivable/actions"><img src="https://github.com/joelbutcher/laravel-archivable/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://github.styleci.io/repos/301993606"><img src="https://github.styleci.io/repos/301993606/shield?style=flat" alt="""StyleCI"></a>
<a href="https://packagist.org/packages/joelbutcher/laravel-archivable"><img src="https://img.shields.io/packagist/dt/joelbutcher/laravel-archivable" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/joelbutcher/laravel-archivable"><img src="https://img.shields.io/packagist/v/joelbutcher/laravel-archivable" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/joelbutcher/laravel-archivable"><img src="https://img.shields.io/packagist/l/joelbutcher/laravel-archivable" alt="License"></a>
</p>

A simple package for making Laravel Eloquent models 'archivable'. This package allows for the easy archiving of models by creating various macros to be used within method chaining.

## Installation

You can install the package via composer:

```bash
composer require joelbutcher/laravel-archivable
```

## Usage

#### Migrations

The `Archivable` trait works similarly to Laravel's `SoftDeletes` trait. To ensure proper usage of the trait. This package also ships with a helpful macro for Laravel's `\Illuminate\Database\Schema\Blueprint`. To get started, simply add the `archivedAt` macro to your migration, like so:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->unsignedBigInteger('user_id');
    $table->string('title');
    $table->timestamps();
    $table->archivedAt(); // Macro
});
```

#### Eloquent
You can now, safely, include the `Archivable` tait in your eloquent model:
 
``` php
namespace App\Models;

use \Illuminate\Database\Eloquent\Model;

class Post extends Model {

    use Archivable;
    ...
}
```

#### Extensions

The extensions shipped with this trait include; `archive`, `unArchive`, `WithArchived`, `withoutArchived`, `onlyArchived` and can be used accordingly:

```php
$user = User::first();
$user->archive();
$user->unArchive();

$usersWithArchived = User::query()->withArchived();
$onlyArchivedUsers = User::query()->onlyArchived();
```

By default, the global scope of this trait uses the `withoutArchived` extension when the trait is added to a model.

### Testing

Currently, a test suite doesn't exist for this package. However, I will be writing tests in line with Laravel's testing schemes for traits. If you wish to contribute any unit tests of your own, please refer to the [contribution guides](#-contributing) below 

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email joel@joelbutcher.co.uk instead of using the issue tracker.

## Credits

- [Joel Butcher](https://github.com/joelbutcher)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

## Laravel Package Boilerplate

This package was generated using the [Laravel Package Boilerplate](https://laravelpackageboilerplate.com).
