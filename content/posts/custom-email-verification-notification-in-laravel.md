---
title: Custom Email Verification Notification in Laravel
description: For most of the people, Laravel's default configuration works just fine but sometimes we need to tweak it a bit to attain our desired result.
---

Laravel being the most loved Framework by the PHP community offers a vast amount of features and scaffolding out of the box.

For most of the people, Laravel's default configuration works just fine but sometimes we need to tweak it a bit to attain our desired result. And that's fine, as it is said,

> Necessity is the mother of invention.

While not invention for now, but we could still look for alternative and efficient ways to do some operations that would otherwise take a lot of code alterations or file changes. Not to forget,

> Less code is better.

## Getting Started

Laravel [authentication package](https://laravel.com/docs/7.x/authentication#introduction) makes it easier to scaffold the Authentication system into our Laravel applications. With all of its sweetness comes Email verification as well, which makes it easier to verify the Email addresses of our users without having to go through all the hassles. Few people like it the way it is, whereas few require some changes in the emails being sent to their users, *maybe for some personal touch!*

There are multiple ways to do the same. Such as overriding the functions, a.k.a. methods in OOP (Object-Oriented Programming) Paradigm or file creations. While performing all these just to change the text doesn't seem feasible. So, we'd look into another option through which we could add some personal touch to the emails being sent or maybe alter it the way we like it.

## Change Email Verification Text

Laravel provides helpers to customize almost everything and we'd be benefitted through the same helper provided by the `VerifyEmail` class located at `Illuminate\Auth\Notifications\Auth` directory. If we take a look at the signature of `toMail` method provided by the `VerifyEmail` class. We'd notice that it is responsible for sending the verification email to the user. This method makes use of `toMailCallback` static property to allow us to customize it.

```php
/**
 * Build the mail representation of the notification.
 *
 * @param  mixed  $notifiable
 * @return \Illuminate\Notifications\Messages\MailMessage
 */
public function toMail($notifiable)
{
    $verificationUrl = $this->verificationUrl($notifiable);

    if (static::$toMailCallback) {
        return call_user_func(static::$toMailCallback, $notifiable, $verificationUrl);
    }

    return (new MailMessage)
        ->subject(Lang::get('Verify Email Address'))
        ->line(Lang::get('Please click the button below to verify your email address.'))
        ->action(Lang::get('Verify Email Address'), $verificationUrl)
        ->line(Lang::get('If you did not create an account, no further action is required.'));
}
```

We can attach our own function to this property and it will be used to create our custom email template for the `VerifyEmail` notification. The method could be attached to the property using the static `toMailUsing` method located in the same file.

Let's open our `AuthServiceProvider` located at `app\Providers` directory. I've chosen `AuthServiceProvider` and not `AppServiceProvider` because I felt the Email verification is related to the Authentication system but You could still set it in the `AppServiceProvider` and it should work just fine.

The very first thing we'd do is to import the classes which we could do using the code below.

```php
use App\User;
use Illuminate\Auth\Notifications\VerifyEmail;
use Illuminate\Notifications\Messages\MailMessage;
use Illuminate\Support\Facades\Lang;
```

Next, we'd attach our own function to the `toMailCallback` property we discovered previously by passing the closure to the `toMailUsing` method of the `VerifyEmail` class. Insert the code below into the boot method of the service provider and make changes to it based on your desired result.

```php
VerifyEmail::toMailUsing(function (User $user, string $verificationUrl) {
    return (new MailMessage)
        ->subject(Lang::get('Verify Email Address'))
        ->line(Lang::get('Please click the button below to verify your email address.'))
        ->action(Lang::get('Verify Email Address'), $verificationUrl)
        ->line(Lang::get('If you did not create an account, no further action is required.'));
});
```

That should be enough. Finally, if the new user registers into the platform then he should receive the Email Verification mail based on the code we used above.

Last but not least! You might want to read our guide on [Setting up your Laravel app on Shared-Hosting platform](https://www.shade.codes/how-to-deploy-laravel-app-on-shared-hosting/) or You might want to spend a few minutes on understanding how you can [Disable Auto-Login in after Registration in your Laravel application](https://www.shade.codes/disable-auto-login-in-laravel-after-registration/).
