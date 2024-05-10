
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