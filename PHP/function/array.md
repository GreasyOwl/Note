# 陣列

## 陣列操作

### count()
> 取得陣列元素個數
#### #Example:
```
$nums = [5, 4, 9, 11, 5];
print_r(count($nums));
```
#### #Output:
```
5
```

### array_count_values()
> 計算元素重複的次數

### array_keys()
> 取得所有索引鍵
#### #Example:
```
$users = [
    ['id' => 3824, 'name' => 'John', 'age' => 25],
    ['id' => 9477, 'name' => 'Allen', 'age' => 33],
    ['id' => 1825, 'name' => 'Alice', 'age' => 45],
];

$keys = array_keys($users[0]);
print_r($keys);
```
#### #Output:
```
Array
(
    [0] => id
    [1] => name
    [2] => age
)
```

### array_values()
> 取得所有值
#### #Example:
```
$users = [
    ['id' => 3824, 'name' => 'John', 'age' => 25],
    ['id' => 9477, 'name' => 'Allen', 'age' => 33],
    ['id' => 1825, 'name' => 'Alice', 'age' => 45],
];

$values = array_values($users[0]);
print_r($values);
```
#### #Output:
```
Array
(    
    [0] => 3824
    [1] => John
    [2] => 25
)
```

### array_sum()
> 加總所有元素的值
#### #Example:
```
$nums = [5, 4, 9, 11, 5];
print_r(array_sum($nums));
```
#### #Output:
```
34
```

### array_unique()
> 去除重複的值
#### #Example:
```
$users = [3824 => 'John', 9477 => 'Alice', 1825 => 'Bob', 4567 => 'John', 5822 => 'Bob'];
print_r(array_unique($users));
```
#### #Output:
```
Array
(
    [3824] => John
    [9477] => Alice
    [1825] => Bob
)
```

### array_change_key_case()
// 改變字串索引鍵為大寫或小寫

### array_pad()
// 擴充元素的數量，當指定數量大於原來元素數量時，則以指定的值代入，當指定數量小於原來數量則不執行

### range()
// 以連續整數為值，建立一個陣列

### array_reverse()
// 將元素值順序倒轉

### list()
// 指派陣列元素成為變數

### array_column()
> 取得某索引鍵的所有值
#### #Example:
```
$users = [
    ['id' => 3824, 'name' => 'John', 'age' => 25],
    ['id' => 9477, 'name' => 'Allen', 'age' => 33],
    ['id' => 1825, 'name' => 'Alice', 'age' => 45],
];

$names = array_column($users, 'name');
print_r($names);
```
#### #Output:
```
Array
(
    [0] => John
    [1] => Allen
    [2] => Alice
)
```

### array_map()
> 將使用者自定義函式作用到陣列中的每個值上，並返回作用後的陣列
#### #Example:
```
$users = [
    ['id' => 3824, 'name' => 'John', 'score' => 25],
    ['id' => 9477, 'name' => 'Allen', 'score' => 60],
    ['id' => 1825, 'name' => 'Alice', 'score' => 90],
];

$new_users = array_map(function($user) {
    $new_score = $user['score'] + 20;

    if ($new_score > 100) {
        $new_score = 100;
    }

    $user['score'] = $new_score;

    return $user;
}, $users);

print_r($new_users);
```
#### #Output:
```
Array
(
    [0] => Array
        (
            [id] => 3824
            [name] => John
            [score] => 45
        )

    [1] => Array
        (
            [id] => 9477
            [name] => Allen
            [score] => 80
        )

    [2] => Array
        (
            [id] => 1825
            [name] => Alice
            [score] => 100
        )

)
```

## 陣列增加、減少

### array_push()
> 新增元素在陣列最後方
#### #Example:
```
$ids = [1, 2, 3, 4];
array_push($ids, 10);
print_r($ids);
```
#### #Output:
```
Array
(
    [0] => 1
    [1] => 2
    [2] => 3
    [3] => 4
    [4] => 10
)
```

### array_pop()
> 移除陣列最後方元素
#### #Example:
```
$ids = [1, 2, 3, 4];
array_pop($ids);
print_r($ids);
```
#### #Output:
```
Array
(
    [0] => 1
    [1] => 2
    [2] => 3
)
```

## 陣列合併

### array_merge()
> 把多個陣列合併為一個陣列。
>
> 若索引鍵有重複，將以後方的值覆蓋。
>
> 若陣列為數字索引，索引鍵會以連續的方式重新索引 (0、1、2...)
#### #Example:
```
$user = ['id' => 3824, 'name' => 'John'];
$user = array_merge($user, ['name' => 'Amy', 'age' => 55]);
print_r($user);
```
#### #Output:
```
Array
(
    [id] => 3824
    [name] => Amy
    [age] => 55
)
```

## 陣列排序

### sort()
> 對值遞增排序，索引鍵會重新排序
#### #Example:
```
$nums = [5, 4, 9, 65, 14, 22];
sort($nums);
print_r($nums);
```
#### #Output:
```
Array
(
    [0] => 4
    [1] => 5
    [2] => 9
    [3] => 14
    [4] => 22
    [5] => 65
)
```

### asort()
> 對值遞增排序，索引鍵不會重新排序
#### #Example:
```
$users = [3824 => 'John', 9477 => 'Alice', 1825 => 'Bob'];
asort($users);
print_r($users);
```
#### #Output:
```
Array
(
    [9477] => Alice
    [1825] => Bob
    [3824] => John
)
```

### ksort()
> 對索引鍵遞增排序
#### #Example:
```
$users = [3824 => 'John', 9477 => 'Alice', 1825 => 'Bob'];
ksort($users);
print_r($users);
```
#### #Output:
```
Array
(
    [1825] => Bob
    [3824] => John
    [9477] => Alice
)
```

## 陣列搜尋

### in_array()

### array_search()
> 搜尋值，並回傳索引鍵
#### #Example:
```
$users = [3824 => 'John', 9477 => 'Alice', 1825 => 'Bob'];
print_r(array_search('Alice', $users));
```
#### #Output:
```
9477
```

## 陣列篩選

### array_filter()
#### #Example:
```
$users = [
    ['id' => 3824, 'name' => 'John', 'score' => 25],
    ['id' => 9477, 'name' => 'Allen', 'score' => 60],
    ['id' => 1825, 'name' => 'Alice', 'score' => 90],
];

$new_users = array_filter($users, function($user) {
    return $user['id'] < 5000 && $user['score'] >= 60;
});

print_r($new_users);
```
#### #Output:
```
Array
(
    [2] => Array
        (
            [id] => 1825
            [name] => Alice
            [score] => 90
        )

)
```