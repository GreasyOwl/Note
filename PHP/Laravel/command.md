# Laravel 指令

## 建立新專案

### 透過 composer

```shell
> composer create-project --prefer-dist laravel/laravel <project-name>
```

### 透過 laravel

```shell
# 需先利用 composer 安裝 laravel/installer 命令列工具
> composer global require laravel/installer

> laravel new <project-name>
```

## 維護模式

```shell
# 進入維護模式
> php artisan down

# 退出維護模式
> php artisan up
```

## 顯示目前執行的環境

```shell
> php artisan env
```

## 指令說明

```shell
> php artisan help <command-name>
```

## 啟動 php 伺服器

```shell
> php artisan serve
```

## 顯示所有指令

```shell
> php artisan list
or
> php artisan
```

## Model

```shell
# 建立 Model
> php artisan make:model <Table>
```

## Controller

```shell
# 建立 Controller
> php artisan make:controller <Name>Controller

# 建立 Resource Controller
> php artisan make:controller <Name>Controller --resource
```

## Route

```shell
# 顯示所有路由
> php artisan route:list

# 清除路由快取
> php artisan route:clear

# 快取路由
> php artisan route:cache
```

## Migration

```shell
# 建立 Migration
> php artisan make:migration create_<table>_table

# 執行 migrate
> php artisan migrate

# migrate 復原到前一個 Batch 的版本
> php artisan migrate:rollback

Options:
    --step[=STEP]   復原到前N個migrate的版本(不是Batch的版本)

# migrate 版本狀態
> php artisan migrate:status
```

## Middleware

```shell
# 建立 middleware
> php artisan make:middleware <Name>
```

## Request

```shell
# 建立 request
> php artisan make:request <Name>
```

## Seeder

```shell
# 建立 seeder
> php artisan make:seeder <Name>Seeder

# 執行 root seeder (預設為 DatabaseSeeder)
> php artisan db:seed

Options:
    --class[=CLASS]   執行指定的seeder
```

## Cache

```shell
# 移除已編譯的 class 檔案
> php artisan clear-compiled

# 快取 bootstrap 檔案 (php 核心)
> php artisan optimize

# 移除快取 bootstrap 檔案
> php artisan optimize:clear
```

## Tinker

```shell
> php artisan tinker
```