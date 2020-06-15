---
title: Intro to AlpineJS
description: In this quick intro I’ll explain how you can use this library to add some simple javascript functionality to your application. you’ll first see how you’d perform this functionality in vanilla javascript and then i’ll show you how you can simplify that by adding some alpine.
---

I know what you’re probably thinking. Another javascript framework/library. But before you write this one off, perhaps you should take a look at how simple and flexible it is.

Alpine can help you perform some simple javascript functionality in your app without bloat. Instead of reaching for something like Vue or React when you build something that needs a little javascript functionality, alpine might be the clear cut choice.

In this quick intro I’ll explain how you can use this library to add some simple javascript functionality to your application. you’ll first see how you’d perform this functionality in vanilla javascript and then i’ll show you how you can simplify that by adding some alpine.

## What is Alpine

So, what exactly is alpine and what can it be used to build?

Alpine is a minimal framework for implementing javascript behavior in your markup. In other words, it can help you create some cool interactivity in your page by adding a little markup to your elements.

Alpine can really be used to build any kind of interactivity in your page like drop downs, tabs, modals, sliders, and much more.

Before we jump into the examples I want to show you how easy it is to installing Alpine.

## Installing Alpine

The easiest way to use Alpine in your website is to just include the CDN link somewhere in the head of your document.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Intro to Alpine</title>
</head>
<body>

    <script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.x.x/dist/alpine.min.js" defer></script>
</body>
</html>
```

Alternatively, you can install Alpine using NPM:

```bash
npm i alpinejs
```

And then import it into your main javascript file:

```js
import 'alpinejs'
```

Now, that you have Alpine installed we can easily create a simple drop down, but before we jump into that I'll first show you how we would typically create this functionality in Vanilla javascript.

## Dropdown Without Alpine

If you wanted to create a simple javascript dropdown, you will probably need some markup that looks like this:

```html
<div>
    <button id="button">Open Dropdown</button>

    <ul id="dropdown" style="display:none; background:#f1f1f1">
        Dropdown Body
    </ul>
</div>
```

We have a simple button and a dropdown container. Then we'll need to add some javascript to make our dropdown function correctly.

```js
<script>
    let open = false;
    let dropdown = document.getElementById('dropdown');
    let button = document.getElementById('button');

    button.addEventListener('click', function(){

        if(dropdown.style.display == 'none'){
            dropdown.style.display = 'block';
            open = true;
        } else {
            dropdown.style.display = 'none';
            open = false;
        }

    });

    document.body.addEventListener('click', function(e){
        if(e.target.id != button.id && e.target.id != dropdown.id){
            dropdown.style.display = 'none';
            open = false;
         }
    });
</script>
```

Notice, above we've also added a `click` event listener for the body because we need to detect when a user clicks away from the dropdown in order to close it.

Take a look at the example codepen of this functionality below:

https://codepen.io/devdojo/pen/rNxxMej

You can see that this functionality is very simple; however, there is quite a bit of javascript for such little functionality. Let's see how simple we can accomplish this functionality using Alpine.

## Dropdown with Alpine

Creating the same dropdown functionality using Alpine is stupid easy. It's as simple as adding a little bit of markup to your HTML:

```html
<div x-data="{ open: false }">
    <button @click="open = true">Open Dropdown</button>

    <ul x-show="open" @click.away="open = false" style="background:#f1f1f1;">
        Dropdown Body
    </ul>
</div>
```

As long as you include the AlpineJS library in your page, you now have the same functionality without writing a line of custom javascript. Take a look at the codepen example of the dropdown using Alpine below.

https://codepen.io/devdojo/pen/NWxxrXE

In order to get this functionality to work, you'll want to make sure to include the small AlpineJS file in your project. Installing Alpine in your application is very easy as well.

## Conclusion

In the documentation for Alpine, it claims to be the [Tailwind](https://tailwindcss.com) for javascript, which is very true. Alpine allows you to add simple javascript functionality to your website without even writing a line of custom javascript.

You can now create javascript interactions using some simple markdown attributes, be sure to checkout the [github repo](https://github.com/alpinejs/alpine) to learn more about all the cool stuff you can do with Alpine.
