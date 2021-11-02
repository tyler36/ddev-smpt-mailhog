# DDEV with Laravel mail <!-- omit in toc -->

- [](#)

## Installation

This describe steps taken for the project

- Install Laravel

    ```shell
    $ laravel new ddev-smtp-mailhog
    $ php artisan --version
    Laravel Framework 8.68.1
    ```

- Configure DDEV project, accepting defaults

    ```shell
    $ ddev config
    Project name (ddev-smpt-mailhog):
    Docroot Location (public):
    Project Type (laravel):
    ```

- Start project and confirm "Welcome page" is accessible from browser

    ```shell
    ddev launch
    ```

- Configure Laravel for DDEV via updating `.env`

```env
# Use default DDEV database
DB_CONNECTION=mysql
DB_HOST=db
DB_DATABASE=db
DB_USERNAME=db
DB_PASSWORD=db

# Use Mailhog
MAIL_MAILER=smtp
MAIL_HOST=localhost
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
```

## Testing

- Create new mailable

  ```shell
  php artisan make:mail WelcomeMail
  ```

- Add a view `./resources/views/mail/welcome-mail.blade.php`

    ```php
    This is an example
    ```

- Configure the `./app/Mail/WelcomeMail.php` mailable to use the view

    ```php
    public function build()
    {
        return $this->view('mail.wlecome-mail');
    }
    ```

- Create a test route to easier send mail a user

    ```php
    Route::get('/', function () {
        Mail::to('example@example.com')->send(new WelcomeMail());

        return view('welcome');
    });
    ```

- Visiting the route will trigger the mail `vendor/laravel/framework/src/Illuminate/Mail/Mailer.php`

    ```php
    if ($this->shouldSendMessage($swiftMessage, $data)) {
        // This following line is run
        $this->sendSwiftMessage($swiftMessage);

        $this->dispatchSentEvent($message, $data);
    }
    ```
