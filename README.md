# back-end-framework

## day11 2019-4-1

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