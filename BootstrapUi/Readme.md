## نصب پکیج bootstrap ui


### توضیحات 

از این پکیج برای مدیریت پنل سایت استفاده میشود 

### Install Pachage Bootstrap Ui

* مرحله اول

:اگر از لاراول ۸ استفاده میکنید این دستور رو بزنید


```bash
composer require laravel/ui
```

:در غیر این صورت

```bash

composer require laravel/ui:^2.4

```
 
* مرحله دوم

بسته به نیاز خودتون پکیجی رو که میخواید رو نصب کنید

:ما در اینجا از پکیج زیر استفاده میکنیم
‍‍

```bash
php artisan ui bootstrap --auth
```

:دیگر پکیج ها

‍‍
```bash
// Generate basic scaffolding...
php artisan ui bootstrap
php artisan ui vue
php artisan ui react

// Generate login / registration scaffolding...
php artisan ui bootstrap --auth
php artisan ui vue --auth
php artisan ui react --auth
```

* مرحله سوم

:توجه کنید که قبل از وارد کردن دستور زیر پکیج زیر رو نصب کنید

‍‍
```bash

PachageName: Npm

```

[نصب پکیج](https://redcherry.ir/%D8%A2%D9%85%D9%88%D8%B2%D8%B4-%D9%86%D8%B5%D8%A8-laravel-ui-%D8%A7%D8%AD%D8%B1%D8%A7%D8%B2-%D9%87%D9%88%DB%8C%D8%AA-%D9%82%D8%AF%DB%8C%D9%85%DB%8C-%D9%84%D8%A7%D8%B1%D8%A7%D9%88%D9%84/)



