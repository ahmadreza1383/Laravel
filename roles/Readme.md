## شروع کار با پکیج رول

____________________________

__ساخت رول در این مقاله کمی زیاد شرح داده شده است که ممکن است باعث سردرگمی و بی حوصلگی شما شود اگر این مقاله حوصله سر بر است میتوانید از ویدیو زیر استفاده کنید__

[اموزش ویدیو ساخت رول ](https://www.aparat.com/v/ZLrXe/%D8%A2%D9%85%D9%88%D8%B2%D8%B4_spatie_%D8%AF%D8%B1_%D9%84%D8%A7%D8%B1%D8%A7%D9%88%D9%84)

____________________________


### پیش نیاز ها 

اول از همه اگه پکیج رو نصب نکرده اید این اموزش رو ببینید

[نصب پکیج رول ساز](https://github.com/ahmadreza1383/Laravel/tree/Packages/roles)

[نصب پکیج مدیریت پنل](https://github.com/ahmadreza1383/Laravel/tree/Packages/BootstrapUi)

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


‍‍‍
```bash 

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
         $role = Role::create(['name' => 'owner']);
         $permission = Permission::create(['name' => 'owner']);
       


        return $next($request);
        
    }
   }
```

:یعنی به این صورت 


‍‍‍
```bash

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;


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
     $role = Role::create(['name' => 'owner']);
     $permission = Permission::create(['name' => 'owner']);
     
      return $next($request);

}
}
```



:حال به ادرس   کرنل زیر برید 


‍‍‍
```bash

app/Http/kernel.php

```

:سورس زیر را تغییر دهید


‍‍‍
```bash
 protected $routeMiddleware = [
        'auth' => \App\Http\Middleware\Authenticate::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
        'can' => \Illuminate\Auth\Middleware\Authorize::class,
        'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
        'password.confirm' => \Illuminate\Auth\Middleware\RequirePassword::class,
        'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
        'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
        'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
    ];

```

:به این صورت

```bash

 protected $routeMiddleware = [
        'owner' => \App\Http\Middleware\OwnerRole::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
        'can' => \Illuminate\Auth\Middleware\Authorize::class,
        'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
        'password.confirm' => \Illuminate\Auth\Middleware\RequirePassword::class,
        'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
        'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
        'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
    ];

```


__رو برداشتیم  auth در اینجا ما میدلور سازنده رو به ارایه اضافه کردیم و میدلور__



:حال به ادرس زیر برید 


‍‍‍
```bash

app/Http/Controllers/HomeController.php

```

:سورس زیر را تغییر دهید


‍‍‍
```bash

 public function __construct()
    {
        $this->middleware('auth');

    }

```

:به این صورت

```bash

 public function __construct()
    {
        $this->middleware('owner');

    }

```




:دستور زیر رو در تریمنال وارد کنید



‍‍‍
```bash

php artisan serve

```

:در مرورگر خود ادرس زیر رو وارد کنید


```bash 
http://127.0.0.1:8000/register

```

بعد یک ثبت نام انجام دهید



:بعد از اتمام ثبت نام به ادرس زیر برید


```bash 
http://127.0.0.1:8000/login

```

ایمیل و رمز عبور خود را وارد کنید


حالا شما رول سازنده رو  ساختید


### دریافت رول سازنده

:برای دریافت رول سازنده سورس زیر را   تغییر دهید 


```bash

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;


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
     $role = Role::create(['name' => 'owner']);
     $permission = Permission::create(['name' => 'owner']);
     
      return $next($request);

}

}
```


:به این صورت تغییر دهید


```bash

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;


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
     $user =$request->user();

     $user->assignRole('owner');
     
     
     return $next($request);

}
}
```


یکبار دیگر ورود کنید

شما رول سازنده رو دریافت کردید

‍‍
### بررسی رول در هنگام ورود


:برای بررسی هنگام ورود کافیه سورس زیر را به این صورت تغییر دهید 


```bash

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;

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
     $user =$request->user();

     $user->assignRole('owner');
     
     
     return $next($request);

}

}
```




:به این صورت
‍‍‍
```bash

<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;



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

      
        $user =$request->user();



        if($user && $user->hasRole('owner')){

            return $next($request);

        }
        if($user && !($user->hasRole('owner'))){

            Auth::logout();
            return redirect('login');

        }
        // return $next($request);
        return redirect('login');


        return $next($request);


    }
}


```


حال شما به عنوان سازنده میتونید ورود کنید


موفق باشید :)


__اگر نمیتوانید طبق اموزش پیش برید از ویدیو ی زیر استفاده کنید__

[اموزش ویدیو ساخت رول ](https://www.aparat.com/v/ZLrXe/%D8%A2%D9%85%D9%88%D8%B2%D8%B4_spatie_%D8%AF%D8%B1_%D9%84%D8%A7%D8%B1%D8%A7%D9%88%D9%84)



































