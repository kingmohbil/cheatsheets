# This is a Laravel cheat sheet fro common use cases

## To include a partial named

> To include partial create a partials directory in your views directory and it's a convention that the name of the file starts with \_

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

> To create a components create a components directory in your views directory

```php
# views/components/nav.blade.php

@props(['name'])

<h1>{{$name}}</h1>
```

> To pass the name props if it is a text

```php
# views/navigation.blade.php

<x-nav name="hello" />
```

> To pass it as a variable you should prefix the prop with a :

```php
# views/navigation.blade.php

<x-nav :name="$hello" />
```

> To add additional class to the current class value, to add a children we use the $slot variable

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

> You can use a shorthand in laravel

```php
# routes/web.php

# Common Resource Routes:
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
        return view('listing', ['listing' => $listing]);
    }
    else {
        abort('404');
    }

});

# you can use this instead it checks it automatically

Route::get('/listing/{listing}', function(Listing $listing){
        return view('listing', ['listing' => $listing]);
});

```
