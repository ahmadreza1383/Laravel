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
