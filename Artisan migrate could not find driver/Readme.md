### حل خطای pdo_mysql

### عنوان خطا


```bash

  [Illuminate\Database\QueryException] could not find driver (SQL: select * from information_schema.tables where table_schema = homestead and table_name = migrations) [PDOException] could not find driver



```


### شروع حل خطا 

نکته : این روش برای سیستم عامل لینوکس توزیع اوبونتو میباشد

اول از همه وارد فایل زیر بشید



```bash

php.ini 

```

بعد مقادیر زیر رو جسنجو کنید و از حالت کامنت در بیارید

‍‍
```bash

;extension=php_pdo_mysql.dll

;extension=php_mysql.dll

```

برای در اوردن کامنت ; اول رو بردارید


و بعد هم دستور زیر را وارد کنید


‍‍‍
```bash
sudo apt install php-mysql

```

__اتمام__

