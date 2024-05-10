
#### Create new php project

```
composer create-project laravel/laravel example-app
```
#### Run php

```
php artisan serve
```

#### Create new controller

 ```
 php artisan make:controller WelcomeController
 ``` 

#### Create new model

```
php artisan make:model  Note -m
```

-m means also migration files

#### Migrate

```
php artisan migrate
```

#### Create Factory

```
php artisan make:factory NoteFactory --model=Note
```

#### Create Seed

```
php artisan migrate:refresh --seed
```

#### Create routes

routes/web.php

```
    // Route::get('/note', [NoteController::class, 'index'])->name('note.index');
    
    // Route::get('/note/create', [NoteController::class, 'create'])->name('note.create');
    
    // Route::post('/note', [NoteController::class, 'store'])->name('note.store');
    
    // Route::get('/note/{id}', [NoteController::class, 'show'])->name('note.show');
    
    // Route::get('/note/{id}/edit', [NoteController::class, 'edit'])->name('note.edit');
    
    // Route::put('/note/{id}', [NoteController::class, 'update'])->name('note.update');
    
    // Route::delete('/note/{id}', [NoteController::class, 'destroy'])->name('note.destroy');

```

This is equal to whole 7 routes.

```
Route::resource('note', NoteController::class);
```

#### Create View

```
php artisan make:view note.index
php artisan make:view note.create
php artisan make:view note.edit
php artisan make:view note.show
```

#### Create Layout

Create views/components/layout.blade.php

```
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Laravel</title>

    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>

<body class="antialiased">
    @session('message')
        <div class="success-message">
            {{ session('message') }}
        </div>
    @endsession
    {{ $slot }}
</body>

</html>
```

in other blade files use it as 

```
<x-layout>
<h1> hello </h1>
</x-layout>
```

#### Create View