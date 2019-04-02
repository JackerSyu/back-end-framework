# back-end-framework


## day12 2019-4-2

### Notes

- try this useful command like `$ php artisan help make:controller`


-  Generate a resource controller class.
`$ php artisian make:controller PostsController -r`

### laravel 419 error -> CSRF (Cross Site Request Forgery)
- `{{ csrf_field() }}` 
- CSRF 就是在不同的 domain 底下卻能夠偽造出「使用者本人發出的 request」。要達成這件事也很簡單，因為瀏覽器的機制，你只要發送 request 給某個網域，就會把關聯的 cookie 一起帶上去。如果使用者是登入狀態，那這個 request 就理所當然包含了他的資訊（例如說 session id），這 request 看起來就像是使用者本人發出的。 [More -> By Huli](https://blog.techbridge.cc/2017/02/25/csrf-introduction/)


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