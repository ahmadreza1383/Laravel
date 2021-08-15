#  خطای دیتابیس
### عنوان خطا
```bash
SQLSTATE[42S01]: Base table or view already exists: 1050 Table 'users' already exists (SQL: create table users
```

### حل خطا
__مراحل زیر را دنبال کنید__

* در دایرکتوری پروژه خود به ادرس زیر برید
```bash 
app/provider/AppServiceProvider.php
```
* فایل را باز کنید و ابتدای فایل قطعه کد زیر را وارد کنید
```bash 
use Illuminate\Support\Facades\Schema;
```
* تابع بوت رو پبدا کنید مانند سورس زیر:
```bash 

public function boot()
{
    //
}
```

* سورس تابع را به این صورت تغییر دهید :
```bash 
public function boot()
{
    Schema::defaultStringLength(191);
}
```
* حال در دایرکتوری پروژه خود محیط تریمنال رو باز کرده و کد زیر را وارد کنید 

```bash 
composer update
```
