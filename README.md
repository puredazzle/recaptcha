reCAPTCHA
=========

![recaptcha](https://cloud.githubusercontent.com/assets/499192/17246444/6c1d188a-558c-11e6-8017-009392496433.gif)

A [reCAPTCHA](https://developers.google.com/recaptcha/intro) PHP package with optional [Laravel](https://laravel.com/) support. reCAPTCHA protects your website from spam and abuse while letting real people pass through with ease.

```php
use Vinkla\Recaptcha\Recaptcha;

// Create a new recaptcha instance.
$recaptcha = new Recaptcha('site-key', 'secret-key');

// Validate the recaptcha response.
$recaptcha->validate('g-recaptcha-response');
```

[![Build Status](https://img.shields.io/travis/vinkla/php-recaptcha/master.svg?style=flat)](https://travis-ci.org/vinkla/php-recaptcha)
[![StyleCI](https://styleci.io/repos/64472238/shield?style=flat)](https://styleci.io/repos/64472238)
[![Coverage Status](https://img.shields.io/scrutinizer/coverage/g/vinkla/php-recaptcha.svg?style=flat)](https://scrutinizer-ci.com/g/vinkla/php-recaptcha/code-structure)
[![Quality Score](https://img.shields.io/scrutinizer/g/vinkla/php-recaptcha.svg?style=flat)](https://scrutinizer-ci.com/g/vinkla/php-recaptcha)
[![Latest Version](https://img.shields.io/github/release/vinkla/recaptcha.svg?style=flat)](https://github.com/vinkla/recaptcha/releases)
[![License](https://img.shields.io/packagist/l/vinkla/recaptcha.svg?style=flat)](https://packagist.org/packages/vinkla/recaptcha)

## Installation

Require this package, with [Composer](https://getcomposer.org/), in the root directory of your project.

```bash
composer require vinkla/recaptcha
```

> The next steps are optional. They're only required if you want to use this package with Laravel.

Add the service provider to `config/app.php` in the `providers` array.

```php
Vinkla\Recaptcha\RecaptchaServiceProvider::class
```

If you want you can use the [facade](http://laravel.com/docs/facades). Add the reference in `config/app.php` to your aliases array.

```php
'Recaptcha' => Vinkla\Recaptcha\Facades\Recaptcha::class
```

## Configuration

To use reCAPTCHA with Laravel, you'll need to publish all vendor assets:

```bash
php artisan vendor:publish
```

This will create a `config/recaptcha.php` file in your app that you can modify to set your configuration. Also, make sure you check for changes to the original config file in this package between releases.

#### Site Key

The site key is used for the HTML form field. Which you can add to your views with the `recaptcha_field()` helper function.

#### Secret Key

The secret key is used to communication between your application and Google. Be sure to keep it a secret.

## Usage

First you'll need to add the Google script to your views just before the closing `</head>` tag. You may [select language code](https://developers.google.com/recaptcha/docs/display#config) parameter to the query which is named `hl`. [See a full list of accepted language codes here](https://developers.google.com/recaptcha/docs/language).

```html
<script src="https://google.com/recaptcha/api.js?hl=en"></script>
```

Then you'll need to create a new `Vinkla\Recaptcha\Recaptcha` instance.

```php
use Vinkla\Recaptcha\Recaptcha;

$recaptcha = new Recaptcha('site-key', 'secret-key');
```

To validate a the response from the form you can use the `validate()` method.

```php
use Vinkla\Recaptcha\Exceptions\UnverifiedRecaptchaException;

try {
    $recaptcha->validate('g-recaptcha-response');
} catch (UnverifiedRecaptchaException $e) {
    // If the validation fails.
}
```

To display the reCAPTCHA field in your form you may add like this.

```html
<div class="g-recaptcha" data-sitekey="your-site-key"></div>
```

## Laravel

If you've installed this package in you Laravel application you may also use the facade class.

```php
use Vinkla\Recaptcha\Facades\Recaptcha;

Recaptcha::validate('g-recaptcha-response');
```

There is also an helper method to add the reCAPTCHA field in your form without having to add the site key manually.

```php
{!! recaptcha_field() !!}
```

## Documentation

If you want to to read more about reCAPTCHA, I'd suggest you [head over to the official documentation](https://developers.google.com/recaptcha/intro).

## License

reCAPTCHA is licensed under [The MIT License (MIT)](LICENSE).
