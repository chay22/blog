---
layout: post
title:  "Laravel: Variable 'sql_mode' can't be set to the value of 'NO_AUTO_CREATE_USER'"
author: "Chay"
---

Since version 8.0.11, MySQL removed the `NO_AUTO_CREATE_USERS` mode. So, if you're working with Laravel with MySQL as
your database driver. And is using strict mode. And also providing your own modes in `config/database.php`,
you would get following error thrown on your screen.

![Laravel NO_AUTO_CREATE_USER error thrown on debug mode](/assets/images/no_auth_create_user-laravel-error.png)

Prior to Laravel 5.5, if you don't provide yourself a customized sql modes on `config/database.php` and set the `strict_mode` to `true`,
you would get similar error as above figure if you use MySQL 8.0.11.

Since Laravel version 5.5 and above default `strict_mode` still include the `ONLY_FULL_GROUP_BY` mode which is known being incompatible 
with Eloquent, you would need to configure the sql mode inside `config/database.php` yourself using the following:

````
'mysql' => [
    // ...
    
    'strict' => true,
    'modes' => [
      'STRICT_TRANS_TABLES',
      'NO_ZERO_IN_DATE',
      'NO_ZERO_DATE',
      'ERROR_FOR_DIVISION_BY_ZERO',
      'NO_ENGINE_SUBSTITUTION',
    ]
],
````
