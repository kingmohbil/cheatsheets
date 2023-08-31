# This is a cheat sheet for artisan command line tool

## Migrations

### To create a table using artisan they would be created in the migrations folder

```properties
php artisan make:migration <migration name>
```

### To run the migrations and execute them

```properties
php artisan migrate
```

### To run the migrations again

```properties
php artisan migrate:refresh
```

### To run the migrations and seed them again

```properties
php artisan migrate:refresh --seed
```

## Factories

### To create a factory to create a fake data

```properties
php artisan make:factory <factory name>
```

### To seed the fake data from the seeders folder

```properties
php artisan seed
```

## Models

### This command is used to generate a model using the cli in Laravel

```properties
php artisan make:model <model Name>
```
