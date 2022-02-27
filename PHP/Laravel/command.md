# Laravel指令
## 建立新專案
### 透過composer
```
> composer create-project --prefer-dist laravel/laravel 專案名稱
```

### 透過laravel
```
# 需先利用composer安裝laravel/installer命令列工具
> composer global require laravel/installer

> laravel new 專案名稱
```

## 啟動網頁伺服器
```
> php artisan serve
```

## Model
```
# 建立Model
> php artisan make:model <Table名稱>
```

## Controller
```
# 建立Controller
> php artisan make:controller <Controller名稱>Controller

# 建立Resource Controller
> php artisan make:controller <Controller名稱>Controller --resource
```

## Route
```
# 顯示所有路由
> php artisan route:list

# 清除路由快取
> php artisan route:clear

# 快取路由
> php artisan route:cache
```

## Migration
```
# 建立Migration
> php artisan make:migration create_<table名稱>_table

# 執行migrate
> php artisan migrate

# migrate復原到前一個Batch的版本
> php artisan migrate:rollback

Options:
    --step[=STEP]   復原到前N個migrate的版本(不是Batch的版本)

# migrate版本狀態
> php artisan migrate:status
```

## Middleware
```
# 建立middleware
> php artisan make:middleware <Middleware名稱>
```

## Request
```
# 建立request
> php artisan make:request <Request名稱>
```
