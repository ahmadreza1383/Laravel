## نصب پکیج bootstrap ui


### توضیحات 

از این پکیج برای مدیریت پنل سایت استفاده میشود 

### Install Pachage Bootstrap Ui

 __مرحله اول__

:اگر از لاراول ۸ استفاده میکنید این دستور رو بزنید


```bash
composer require laravel/ui
```

:در غیر این صورت

```bash

composer require laravel/ui:^2.4

```
 
__مرحله دوم__

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

 __مرحله سوم__

:توجه کنید که قبل از وارد کردن دستور زیر پکیج زیر رو نصب کنید

‍‍
```bash

PachageName: Npm

```

[نصب پکیج](https://docs.npmjs.com/cli/v6/commands/npm-install/)

:در صورت نصب موفقیت امیز دستور زیر را وارد کنید
‍‍‍
```bash 

npm install


```

:و بعدش هم این دستور

```bash 

npm run dev

```

__مرحله چهارم__ 

:دستور زیر را بزنید 
‍‍‍
```bash
php artisan serve
```

:بعد به ادرس زیر برید
‍‍‍
```bash
http://127.0.0.1:8000/login
```

در اینجا پورت ما 8000 بوده است


اگر ظاهر سایت __نامناسب__ بود و رنک ها و فونت ها قرار نکرفته بودند  مرحله 5 رو دنبال کنید


__مرحله پنج__

:دوباره دستور زیر را وارد کنید 

```bash
npm install 
```

بعد دوباره تست کنید

__موفق باشید :)__

