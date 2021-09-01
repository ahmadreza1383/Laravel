## شروع کار با پکیج رول

### پیش نیاز ها 

اول از همه اگه پکیج رو نصب نکرده اید این اموزش رو ببینید

[نصب پکیج رول ساز](https://github.com/ahmadreza1383/Laravel/tree/Packages/roles)

### توضیحات 

در اینجا ما قصد داریم که یک رول به نام سازنده ایجاد کنیم که فقط کاربرانی که این رول را دارند اجازه ورود به پنل مدیریت سایت را داشته باشند

### شروع کار 

:اول از همه وارد ادرس زیر بشوید
‍‍‍
```bash 
app/Models/User.php
```


:در کلاس زیر چیزی همانند سورس پایین داریم

‍‍‍
```bash

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;


class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable;
}

```

__در اینجا فقط سورسی که باهاش کار داریم قرار داده شده است و به علت جلوگیری از اشغال بیش از حد مقاله بوده است__ 




 : بهش اضافه  میکنیم use  اول از همه یک 

‍
```bash 

use Spatie\Permission\Traits\HasRoles;

```


 اضافه میکنیم  use و همچنین در داخل کلس هم به مقادیر یک        

به این صورت 

```bash

    use HasApiTokens, HasRoles ,HasFactory, Notifiable;

```


:در واقع سورس ما در اخر به این صورت در میاید


```bash

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;
use Spatie\Permission\Traits\HasRoles;


class User extends Authenticatable
{
    use HasApiTokens, HasRoles ,HasFactory, Notifiable;
}

```




### ساخت رول سازنده


خب تا اینجا ما نصف کار رو پیش بردیم حالا لازمه که یک رول برای وبسایت خود بسازیم

 : میسازیم  middleware اول از همه یک  

‍‍
```bash

php artisan make:middleware OwnerRole

```

:بعد از ساخت به ادرس زیر برید

```bash

app/Http/Middleware/OwnerRole.php

```

:چیزی همانند سورس زیر است


‍‍‍```bash 

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class OwnerRole
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle(Request $request, Closure $next)
    {


        return $next($request);


    }
}

```


 : های زیر را  بهش اضافه  میکنیم  use   


```bash

use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;

```


:سورس زیر را در کلس بهش اضافه میکنیم 


```bash



 public function handle(Request $request, Closure $next)
    {
         $role = Role::create(['name' => 'owner']);
         $permission = Permission::create(['name' => 'owner']);
       


        return $next($request);
        
    }
```



































