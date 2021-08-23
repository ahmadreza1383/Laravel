## نصب پکیج spatie

__مقدمات برای نصب__

اول از همه چک کنید ببینید تو ادرس زیر همچین فایل داری یا خیر 
```bash
config/permission.php
```



اگه همچین فایل داشتید پاکش کنید

__install spatie__


* مرحله اول
‍
```bash
 composer require spatie/laravel-permission
 ```

* مرحله دوم

به صورت پیشفرض این دستور قرار میگیرد اما اگر نبود شما اون رو قرار دهید
‍‍‍
```bash
address : config.app.php
```

```bash 
'providers' => [
    // ...
    Spatie\Permission\PermissionServiceProvider::class,
];
```


* مرحله سوم

```bash
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"

```


* مرحله چهارم 

اگر پکیج مدیریت  رو نصب نکرده اید پیشنهاد ما این است که نصبش کنید

‍‍‍‍
```bash
PackageName : bootstrap ui
```

(نصب پکیج مدیریت)[]

* مرحله اخر


```bash

 php artisan migrate

```
