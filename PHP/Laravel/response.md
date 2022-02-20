# Response

## 範例
```
# 回傳字串
return 'Hello World';

# 回傳陣列
return [1, 2, 3];

# 回傳header、view
return response()
->header('Content-Type', 'text/plain')
->view('welcome');

# 回傳json
return response()->json([
    'name' => 'Abigail',
    'state' => 'CA',
]);

# 強制使用者的瀏覽器下載檔案
return response()->download($pathToFile, $name, $headers);

# 在使用者的瀏覽器顯示檔案
return response()->file($pathToFile, $headers);

# 轉址
return redirect('/');
```
