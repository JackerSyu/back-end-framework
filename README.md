# back-end-framework

## day11 2019-4-1

### laravel/installer 

    composer global require laravel/installer

-> path setting : https://ithelp.ithome.com.tw/articles/10210574?sc=rss.qu

### basic routing 

- get to the laravel folder 
- and input `$ php artisan serve` in command line
- then you can get to your web page
- check the **web.php** on **routes folder** which  correspond to the **views** folder 

### @yield
- create a **layout.blade.php** in **views** 
- design the layout of html in layout.blade.php
- and put **@yield('content')** wherever you want 
- also you can put multiple @yield, for example you can set **@yield('title', 'timothy')** in the title 
- go to the **welcome.blade.php** and put the **@extends('layout')** on the first line 
- then **@section('content')** [html format here]  **@endsection**

```php
@extends('layout')

@section('title', 'welcome')
    


@section('content')
    <h1>welcome !</h1>
@endsection
```

### Controller 

`$ php artisan make:controller "name"`

- check out app/Http/Controllers

```php
class PagesController extends Controller
{
    public function home ()
    {
        $tasks = [
            'Go to the school',
            'Go to the store',
            'Go to work'
        ];
    
        return view('welcome', [
            'tasks' => $tasks,
            'foo' => 'Timothy'
        ]); 
    }

    public function about ()
    {
        return view('about');
    }

    public function contact()
    {
        return view('contact');
    }
}

```

- change the web.php in routes 

```php
Route::get('/', 'PagesController@home');

Route::get('/about', 'PagesController@about');

Route::get('/contact', 'PagesController@contact');

```


### Migration Problem 

when `$ php artisan migrate `

    Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table `users` add unique `users_email_unique`(`email`))


- go to app/provider/AppServiceProvider.php

add `Schema::defaultStringLength(191);` in the function boot

`use Illuminate\Support\Facades\Schema;`

### Migration instructions

`php artisan migrate`
`php artisan migrate:rollback` to undo the last vesion of database

`php artisan migrate:fresh` to update your change