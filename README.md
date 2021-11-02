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
