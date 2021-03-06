# Startup Framework
The starters framework for your MVC application.

### Configure the router

The router can be found under file `public/index.php`. No worries, the router will get its own file in the future.

You can currently only define a `get` and `post` route. The router accepts two paramaters, which will be the path and callback.
#### You can use a closure:
```php
$app->router->get('/home', function () {
    return 'This is the home route.';
});
```

#### Or attach a router to a controller and method.
```php
$app->router->get('/example', [\App\Controllers\ExampleController::class, 'index']);
```
This can also be done for `post`.
```php
$app->router->post('/example', [\App\Controllers\ExampleController::class, 'store']);
```

### Create a controller
The controllers can be found under directory `app/Controllers`. The authentication controllers are included as default 
and can be adjusted. The controllers are always an expanding the class `app/General/Controller.php`.
If you want to return a view from the method, you can use the function `view()` that accepts a path and parameters 
which is by default an empty array.

#### Make method index return view `home.php`:
```php
public function index(): array|string
{
    return $this->view('home');
}
```
#### If the view is located in a directory inside `view`, use a forward slash:
```php
return $this->view('directory/home');
```
#### Sending parameters into the view:
```php
$params = [
    'foo' => 'bar',
    'hello_world'
];

return $this->view('home', $params);
```
These parameters can be accessed in the view.
#### By an associative array we can access the value of key by a variable:
```php
<?php
echo $foo . ' ' . $params[1];
?>

// Outputs: bar hello_world
```

### Create a view
The views can be found under directory `views`. This directory has standard a `layouts/main.php` file that must be used as default layout for the application.
You can create a new default layout or rename the current one. The default layout holds the `{{ content }}` placeholder. 
This placeholder will automatically be replaced with the given view in the controller.

## Security

If you discover any security related issues, please create an issue.
## Credits

- [Yassine el Fahmi](https://github.com/yassinefahmi)

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.