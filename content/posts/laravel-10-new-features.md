+++
title = 'Laravel 10 new features'
date = 2023-02-15T00:00:00+00:00
draft = false
tags = ['laravel', 'php', 'laravel-10', 'release']
+++

Finally, Laravel 10 is released. It requires PHP >= 8.1. Most of the features are added by the core Laravel team and not by other contributors, and it seems that there are no big changes compared to previous version releases. Let's have a glance.

## New Type Hinting Model

Nuno Maduro, creator of [Pest](https://github.com/pestphp/pest), has added a new PHP style of type hinting and removed the old way of doc-block in all stubs and maybe the codebase. It seems that the change does not have a sensible difference for end-users :)

```php
/**
* Display a listing of the resource.
*/
public function index(): Response
{
    // ...
}
```

## Features with Pennant

Another core member of Laravel, named [Tim MacDonald](https://github.com/timacdonald), has developed a new package named Pennant that makes it easy to publish specific features for specific users. Consider a situation where you have added a new feature and you want to test it on a small chunk of users. The package has introduced a convenient way for that.

```php
use Laravel\Pennant\Feature;
use Illuminate\Support\Lottery;

Feature::define('new-onboarding-flow', function () {
    return Lottery::odds(1, 10);
});
```

## Process Interaction in a simple way

This feature is a little bit funny. I have experience working with the command line `exec`, which we can use to run a program in the OS's shell with PHP like `ls -a`. With this new feature, you can run this kind of command with a better coding interface:

```php
use Illuminate\Support\Facades\Process;

$result = Process::run('ls -la');

return $result->output();
```

## Profile tests

If your tests take too much time to complete (like mine :)), try this feature. It profiles your tests and reports the execution time, which makes it easy to find slow tests.

```bash
php artisan test --profile
```

![Test profiling output](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/e72gtpr9744qtjne6gw3.png)

## Use Pest for testing

If you prefer the Pest PHP testing format for writing your tests, now it is built into Laravel and you can use it easily.

## Command CLI prompts

This feature prompts the user to complete the command if it was not complete. For example, if you run a command like this:

```bash
php artisan make:controller
```

It asks you for the name of the controller. We can accept it from [Jess](https://github.com/jessarcher) :)

## Better Horizon and Telescope

Finally, if you are a fan of one of the above tools, there is a little bit of a face lift on them.

Overall, I think the changes were not big, but that is the open-source world and we have to thank the contributors for their efforts. If you want a new thing, go and write it :) Have a good time.
