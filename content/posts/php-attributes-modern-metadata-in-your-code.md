+++
title = 'PHP Attributes: Modern Metadata in Your Code'
date = 2025-09-11T00:00:00+00:00
draft = false
tags = ['php', 'php8', 'attributes', 'metadata', 'programming']
+++

Since PHP 8, we've had **attributes** — a modern way to add metadata directly to classes, methods, or properties. Think of them like annotations in Java or decorators in Python.

## What are Attributes?

Attributes let you "tag" parts of your code with extra information. Frameworks or libraries can then read these tags at runtime and act on them.

Example:

```php
#[Route('/home', methods: ['GET'])]
class HomeController {
    // ...
}
```

Here, the `Route` attribute describes how this controller should be exposed.

## How Do You Define an Attribute?

Attributes are just classes marked with `#[Attribute]`.

```php
use Attribute;

#[Attribute]
class Route {
    public function __construct(
        public string $path,
        public array $methods = ['GET']
    ) {}
}
```

## How to Read Attributes with Reflection

You can fetch and use attributes at runtime via the **Reflection API**:

```php
$reflection = new ReflectionClass(HomeController::class);

// Get all attributes on the class
foreach ($reflection->getAttributes(Route::class) as $attr) {
    // Turn attribute into a real object
    $route = $attr->newInstance();

    echo $route->path;     // "/home"
    echo implode(',', $route->methods); // "GET"
}
```

This is how frameworks like Symfony or Doctrine process metadata and apply logic automatically.

## Why Use Attributes?

* Cleaner than PHPDoc comments
* More flexible than marker interfaces
* Supported natively by PHP, no hacks needed

## Where Are They Used?

* **Symfony** → `#[Route]` for controllers
* **Doctrine ORM** → `#[Entity]`, `#[Column]` for database mapping
* Custom apps → logging, caching, validation rules

**In short:** Attributes bring structured, modern metadata to PHP. They're concise, powerful, and built right into the language — and with reflection, they let your code adapt based on annotations.
