## نصب پکیج spatie


### توضیحات

از این پکیج برای دسته بندی کاربر ها استفاده میشه 
به عنوان مثال شما میتونید تایین کنید که کدام کاربر ادمین و کدام کاربر نویسنده یا غیره است

### مقدمات برای نصب

اول از همه چک کنید ببینید تو ادرس زیر همچین فایل داری یا خیر اگه همچین فایل داشتید پاکش کنید
 
```bash
config/permission.php
```




### install spatie


* مرحله اول
‍
```bash
 composer require spatie/laravel-permission
 ```

* مرحله دوم

به صورت پیشفرض این دستور قرار __میگیرد__ اما اگر نبود شما اون رو قرار دهید
‍‍‍
```bash
Address : config.app.php
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

اگر پکیج مدیریت  رو نصب نکرده اید پیشنهاد ما این است که __نصبش__ کنید

‍‍‍‍
```bash
PackageName : bootstrap ui
```

[نصب پکیج مدیریت](https://github.com/ahmadreza1383/Laravel/blob/Packages/BootstrapUi/Readme.md)
* مرحله اخر


```bash

 php artisan migrate

```
