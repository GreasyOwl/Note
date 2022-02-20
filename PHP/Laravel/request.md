# Request

## 範例
```
# 取得所有參數
$request->all()

# 取得特定參數
$request->input('name');

# 取得特定參數，並給預設值
$request->input('name', Bob);

# 只取得網址列參數
$request->query();

# 取得uri
$request->path()

網址: http://example.com/foo/bar
取得: foo/bar
```
