# Buxus - A PHP Command Bus

[![Build Status](https://travis-ci.org/0x13a/buxus.svg?branch=master)](https://travis-ci.org/0x13a/buxus)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Coverage Status](https://coveralls.io/repos/github/0x13a/buxus/badge.svg?branch=master)](https://coveralls.io/github/0x13a/buxus?branch=master)

## Why a PHP Command Bus

- Keeps Application logic separated from Domain logic
- Commands enforce discoverability
- Command Handlers enforce Single Responsibility Principle
- Can be easily extended (decorated)

Read more here [https://medium.com/@0x13a/building-a-php-command-bus-a65e6ae6a6ac](https://medium.com/@0x13a/building-a-php-command-bus-a65e6ae6a6ac)

## Prerequisites

- PHP >= 7.x
- Composer

## Install

```sh
composer require 0x13a/buxus
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

$loggedCommandBus->dispatch(new CreateProductCommand('beer'));
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

- No `NULL` is used
- `final` classes by default (*Composition over inheritance*)
- [Object Calisthenics](https://medium.com/web-engineering-vox/improving-code-quality-with-object-calisthenics-aa4ad67a61f1)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design))
- Immutable data structures


## License

Buxus is licensed under the MIT license. See [License File](LICENSE) for more information

