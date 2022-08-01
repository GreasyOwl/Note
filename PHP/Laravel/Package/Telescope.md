# Telescope Guide

## 目錄

- [安裝步驟 (local)](#安裝步驟-local)
- [額外設定](#額外設定)
- [使用方式](#使用方式)

## 安裝步驟 (local)

### 1. composer telescope

```shell
> composer require laravel/telescope --dev
```

### 2. publish telescope's assets

```shell
> php artisan telescope:install
```

### 3. 使用另外的資料庫 (非必要)

```php
📁config\database.php
新增連線方式

'connections' => [

    'telescope' => [
        'driver' => 'mysql',
        'host' => env('TELESCOPE_DB_HOST', '127.0.0.1'),
        'port' => env('TELESCOPE_DB_PORT', '3306'),
        'database' => env('TELESCOPE_DB_DATABASE'),
        'username' => env('TELESCOPE_DB_USERNAME'),
        'password' => env('TELESCOPE_DB_PASSWORD'),
        'unix_socket' => env('TELESCOPE_DB_SOCKET', ''),
        'charset' => 'utf8mb4',
        'collation' => 'utf8mb4_unicode_ci',
        'prefix' => '',
        'prefix_indexes' => true,
        'strict' => true,
        'engine' => null,
        'options' => extension_loaded('pdo_mysql') ? array_filter([
            PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
        ]) : [],
    ],

],
```

```php
📁config\telescope.php
修改連線方式

'storage' => [
    'database' => [
        'connection' => env('TELESCOPE_DB_CONNECTION', 'telescope'),
        'chunk' => 1000,
    ],
],
```

```javascript
📁.env.example
新增環境設定

TELESCOPE_DB_CONNECTION=telescope
TELESCOPE_DB_HOST=127.0.0.1
TELESCOPE_DB_PORT=3306
TELESCOPE_DB_DATABASE=telescope
TELESCOPE_DB_USERNAME=root
TELESCOPE_DB_PASSWORD=
```

### 4. migrate telescope

```shell
> php artisan migrate
```

### 5. 移除 app 設定檔的 TelescopeServiceProvider

```diff
📁config\app.php
'providers' => [
-    App\Providers\TelescopeServiceProvider::class,
],
```

### 6. 註冊 telescope's service providers

```php
📁app\Providers\AppServiceProvider.php

public function register()
{
    if ($this->app->environment('local')) {
        $this->app->register(\Laravel\Telescope\TelescopeServiceProvider::class);
        $this->app->register(TelescopeServiceProvider::class);
    }
}
```

### 7. 防止 telescope package 被 auto discover

```json
📁composer.json

{
    "extra": {
        "laravel": {
            "dont-discover": [
                "laravel/telescope"
            ]
        }
    },
}
```

### 8. 升級 telescope 版本時，自動重新 publish telescope's assets

```json
📁composer.json

{
    "scripts": {
        "post-update-cmd": [
            "@php artisan telescope:publish --ansi"
        ]
    },
}
```

### 9. 設定排程清除資料 (非必要)

```php
📁app\Console\Kernel.php
設定排程頻率

protected function schedule(Schedule $schedule)
{
    // 每日清除超過24小時的DB資料
    $schedule->command('telescope:prune')->daily();

    // or

    // 每日清除超過N小時的DB資料
    $schedule->command('telescope:prune --hours=N')->daily();
}
```

```shell
Ubuntu
// 修改排程
> crontab -e
* * * * * cd /var/www/html/{your-project} && php artisan schedule:run >> /dev/null 2>&1
```

### 10. 環境設定範例

```javascript
📁.env.example

TELESCOPE_DB_CONNECTION=telescope
TELESCOPE_DB_HOST=127.0.0.1
TELESCOPE_DB_PORT=3306
TELESCOPE_DB_DATABASE=telescope
TELESCOPE_DB_USERNAME=root
TELESCOPE_DB_PASSWORD=
TELESCOPE_ENABLED=true
TELESCOPE_PATH=telescope
```

## 額外設定

### 自訂標籤

```php
📁config\telescope.php

/*
|--------------------------------------------------------------------------
| Telescope 自訂標籤
|--------------------------------------------------------------------------
|
| 以逗號區別各個標籤
|
*/

'custom_tags' => explode(',', env('TELESCOPE_CUSTOM_TAG', 'backend')),
```

```php
📁app\Providers\TelescopeServiceProvider.php

public function register()
{
    Telescope::tag(function (IncomingEntry $entry) {
        $tags = [];
        $customTags = config('telescope.custom_tags');
        if (!empty($customTags)) {
            foreach ($customTags as $tag) {
                $tags[] = $tag;
            }
        }

        return $tags;
    });
}
```

## 使用方式

### 1. 設定環境

```javascript
📁.env

APP_ENV=local

TELESCOPE_DB_CONNECTION=telescope
TELESCOPE_DB_HOST=127.0.0.1
TELESCOPE_DB_PORT=3306
TELESCOPE_DB_DATABASE=telescope
TELESCOPE_DB_USERNAME=root
TELESCOPE_DB_PASSWORD=
TELESCOPE_ENABLED=true
TELESCOPE_PATH=telescope
```

### 2. 網址輸入 {your-domain}/telescope

```
可自行變更路徑:
📁.env
TELESCOPE_PATH=telescope
```
