+++
title = 'Mock Config in Laravel'
date = 2022-09-03T00:00:00+00:00
draft = false
tags = ['laravel', 'php', 'testing', 'mocking']
+++

Hi all. If you are testing your application and you need to make your config constant or change it to a specific value for testing, you can mock it simply!

The `Config` facade of Laravel has a method named `set()` which overwrites the default value of configs like this:

```php
Config::set('name', 'Laravel');
```

So in a testing environment, you can do something like this:

```php
public function test_that_home_page_is_working()
{
    Config::set('name', 'Laravel');
    $this->get('/')->assertSee("Laravel");
}
```

Generally, **Laravel facades** have several benefits because of their testability. You can **[Mock](https://laravel.com/docs/9.x/mocking)** all facades of Laravel easily. Also, if you want to have deeper knowledge about testing tools, you can take a look at [PHP Mockery](http://docs.mockery.io/en/latest/).
