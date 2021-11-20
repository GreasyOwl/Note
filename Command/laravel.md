# 建立新專案
## 透過composer
```
composer create-project --prefer-dist laravel/laravel 專案名稱
```

## 透過laravel
```
# 需先利用composer安裝laravel/installer命令列工具
composer global require laravel/installer

laravel new 專案名稱
```

# 啟動網頁伺服器
```
php artisan serve
```

# Model
```
# 建立Model
php artisan make:model 資料表名稱
```

# Controller
```
# 建立Controller
php artisan make:controller Controller名稱
```