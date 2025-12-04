+++
title = 'Activate links of Laravel Blade based on current route name'
date = 2022-05-13T00:00:00+00:00
draft = false
tags = ['laravel', 'blade', 'php', 'package']
+++

Consider a navigation menu with a bunch of links and you are trying to activate them based on the current active route name. In a normal case, you have to return the `currentRouteName()` from the controller or maybe in a view composer or any other place. I have written a simple Laravel composer package that makes it a little bit simpler.

You can take a look at it here: [https://github.com/hamidhaghdoost/active](https://github.com/hamidhaghdoost/active).

For installation, use the composer require command like this:

```bash
composer require tuytoosh/active
```

Then use the `@active()` directive in your blade files.

```html
<a href="#" class="@active('home')">Home page</a>
```

Without this package, you have to write something like this:

```html
<a href="#" class="@if(Route::getCurrentRouteName() == 'home') active @endif">Home page</a>
```

After version `1.7.0`, you are able to define an array of route patterns like this:

```html
class="@active(['admin.dashboard', 'user.dashboard'])"
```

If you find it useful, give it a star :)

Thank you for reading.
