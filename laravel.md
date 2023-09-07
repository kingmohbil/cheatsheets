# This is a Laravel cheat sheet fro common use cases

## To include a partial named

### To include partial create a partials directory in your views directory and it's a convention that the name of the file starts with `'_'`

```php
# views/partials/_hero.blade.php

<nav>
    <ul>
        <li>
            List item 1
        </li>
        <li>
            List item 2
        </li>
        <li>
            List item 3
        </li>
    </ul>
</nav>
```

```php
# views/home.blade.php

@inlude('partials/_hero')
```

### To create a components create a components directory in your views directory

```php
# views/components/nav.blade.php

@props(['name'])

<h1>{{$name}}</h1>
```

### To pass the name props if it is a text

```php
# views/navigation.blade.php

<x-nav name="hello" />
```

### To pass it as a variable you should prefix the prop with a :

```php
# views/navigation.blade.php

<x-nav :name="$hello" />
```

### To add additional class to the current class value, to add a children we use the $slot variable

```php

# views/components/nav.blade.php

<div {{attributes->merge(['class' => 'grid-6'])}}>
    {{$slot}}
</div>

```

```html
<!-- views/navigation.blade.php -->

<x-nav class="bg-red">
  <h1>welcome</h1>
</x-nav>

<!-- it is equivalent to -->

<div class="grid-6 bg-red">
  <h1>welcome</h1>
</div>
```

### You can use a shorthand in laravel

```php
# routes/web.php

# Common Resource Routes that should be in the controller:
# index - Show all listings
# show - Show single listing
# create - Show form to create a bew listing
# store - Store new listing
# edit - Show form to edit listing
# update - Update listing
# destroy - Delete listing

Route::get('/listing/{id}', function($id){
    $listing = Listing::find($id);
    if ($listing) {
        return view('listing', ['listing' =### $listing]);
    }
    else {
        abort('404');
    }

});

# you can use this instead it checks it automatically

Route::get('/listing/{listing}', function(Listing $listing){
        return view('listing', ['listing' =### $listing]);
});

```

### To create a controller using artisan

```properties
php artisan make:controller <controller name>
```

### For passing the controller into the handler.

```php
# web.php

Route::get('/', [controller_name::class, 'function name'])

```

### To get the request object you have two ways they both get the same result

```php
# dependency injection

Route::get('/', function(Request $request){

    # access the query tag
    echo $request->tag;

    # or
    echo $request['tag'];
})

# or the request helper function

Route::get('/', function(){
   # access the query tag
    echo request()->tag;

    # or
    echo request('tag');
})

```

### For using filters on the model using `php Listing::latest()->filter([filter])->get()` we need to define a scope filter method on the model

```php
# Listing.php

class Listing extends Model {
    public function scopeFilter($query, array $filters) {
        if($filters['tag'] ?? false) {
            $query->where('tags', 'like', "%{$filters['tag']}%")
        }
    }
};
```

### To send forms in laravel you should include a csrf directive under the form like so

```php
# form.blade.php

<form method="POST" action="/">
  @csrf
  <input name="name">
</form>
```

### For validating the form fields you can use `php $request->validate()` like so, for further explanation you can visit the docs [here](https://laravel.com/docs/10.x/validation#quick-writing-the-validation-logic).

```php

$validatedData = $request->validate([
    'title' => ['required', 'max:255'],
    # specify the table name in the database and the column
    'company' => ['required', Rule::unique('listings', 'company')]
]);
```

### if you encountered an error in the form submission you can show it, and access the message content like so

```php

<input name="title" placeholder="Page title">
@error('title')
<p class="error">{{$message}}</p>
@enderror
```

### To keep the values after submitting the form use the old method

```php
<input name="title" placeholder="Page title" value="{{old('title')}}">
```

### Allowing mass assignment in laravel read about it [here](https://codewithtravel.medium.com/laravel-mass-assignment-guarded-or-fillable-7c3a64b49ca6).

```php

# Listing.php

class Listing {
    protected $fillable = [<column names>];
};

```

### For adding text as a message we added it to the session we do it like this

```php

return redirect('/')->with('message', 'Listing created successfully');

```

### For showing the message

```php




```
