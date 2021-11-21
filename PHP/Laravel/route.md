# 路由
## 常用路由方法
```
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
Route::any($uri, $callback);
Route::resource($uri, $callback);
```
## 範例
```
# 一般
Route::get('/', function () {
    return view('welcome');
});

Route::get('/user', [UserController::class, 'index']);

# resource
Route::resource('user', UserController::class);

# group
Route::group([
    'middleware' => ['auth'], // 中介層
    'prefix' => 'admin', // URI前綴，ex: /admin/car
    'as' => 'admin.', // 路由名稱前綴，ex: admin.car
], function () {
    Route::get('/car', [CarController::class, 'index'])->name('car');
    Route::resource('user', UserController::class);
});

註: laravel 8 已移除namespace屬性
```