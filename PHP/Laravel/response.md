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
## 轉址到某個路徑
return redirect('/'); // 相等於 redirect()->to('/')
## 轉址到某個路由名稱
return redirect()->route();
## 轉址回前一頁
return back(); // 相等於 redirect()->back()
## 轉址到目前頁面
return redirect()->refresh();
## 轉址到外部URL，不使用預設的URL驗證
return redirect()->away();
## 轉址到某個controller的function
return redirect()->action();
## 當user造訪一個未通過身分驗證的route時，會儲存要前往的route，再轉址登入頁
return redirect()->guest();
## 當user成功通過身分驗證後，會轉址到guest()儲存的route
return redirect()->intended();
```
