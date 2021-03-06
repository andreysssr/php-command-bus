# Buxus - A PHP Command Bus

[![Build Status](https://travis-ci.org/0x13a/buxus.svg?branch=master)](https://travis-ci.org/0x13a/buxus)
[![License](https://poser.pugx.org/0x13a/buxus/license)](https://packagist.org/packages/0x13a/buxus)
[![Coverage Status](https://coveralls.io/repos/github/0x13a/buxus/badge.svg?branch=master)](https://coveralls.io/github/0x13a/buxus?branch=master)
[![composer.lock](https://poser.pugx.org/0x13a/buxus/composerlock)](https://packagist.org/packages/0x13a/buxus)

## Why a PHP Command Bus

- Keeps Application logic separated from Domain logic
- Commands enforce discoverability
- Command Handlers enforce Single Responsibility Principle
- Can be easily extended (decorated)

Read more here [Building a PHP Command Bus](https://medium.com/@0x13a/building-a-php-command-bus-a65e6ae6a6ac)

## Prerequisites

- PHP >= [7.x](http://php.net/manual/en/migration70.php)
- [Composer](https://getcomposer.org) - Dependency Manager for PHP

## Install

Install using composer

```sh
composer require 0x13a/buxus
```

Run test suite

```sh
vendor/bin/phpunit
```

Check code style

```sh
composer check-cs
```

Check Object Calisthenics rules

```sh
composer check-calisthenics
```

## Getting started

You can simply define your `Command => CommandHandler` map and then instantiate your command bus, ready to use.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

$commandHandlerMap = [
    CreateProductCommand::class => new CreateProductHandler()
];

$standardCommandBus = new \Buxus\Bus\StandardCommandBus(
    new \Buxus\Handler\StandardCommandHandlerLocator(
        new \Buxus\Map\InMemoryCommandHandlerMap($commandHandlerMap)
    )
);

$standardCommandBus->dispatch(new CreateProductCommand('beer'));
```

## Extending Command Bus

If you want to extend the default Command Bus functionality, you can decorate it, creating a new one based on your needs.

See [Decorator Pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

$commandHandlerMap = [
    CreateProductCommand::class => new CreateProductHandler()
];

$standardCommandBus = new \Buxus\Bus\StandardCommandBus(
    new \Buxus\Handler\StandardCommandHandlerLocator(
        new \Buxus\Map\InMemoryCommandHandlerMap($commandHandlerMap)
    )
);

$loggedCommandBus = new LoggedCommandBus(
    $standardCommandBus,
    new Logger()
);

$loggedCommandBus->dispatch(new CreateProductCommand('beer'));
```



## In this project

- [No `NULL` is used](https://medium.com/web-engineering-vox/why-null-references-are-a-bad-idea-17985942cea)
- `final` classes by default (*Composition over inheritance*)
- [Object Calisthenics](https://medium.com/web-engineering-vox/improving-code-quality-with-object-calisthenics-aa4ad67a61f1)
- [SOLID Principles](https://medium.com/web-engineering-vox/how-to-write-solid-code-that-doesnt-suck-2a3416623d48)
- [Immutable data structures](https://medium.com/web-engineering-vox/3-benefits-of-using-immutable-objects-886ca2c56e85)


## License

Buxus is licensed under the MIT license. See [License File](LICENSE) for more information

