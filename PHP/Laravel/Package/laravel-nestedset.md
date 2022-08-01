# laravel-nestedset

## 目錄

- [基本須知](#基本須知)
- [需求](#需求)
- [範例](#範例)
- [參考](#參考)

## 基本須知

- 適用於 tree 結構資料表 (ex: menu、分類)
- 使用的演算法: <a href="http://mikehillyer.com/articles/managing-hierarchical-data-in-mysql/" target="_blank">Modified Preorder Tree Traversal</a>

## 需求

- 安裝

  ```shell
  > composer require kalnoy/nestedset
  ```

- 資料表

  - 必要欄位

    ```sql
    `id` int unsigned NOT NULL AUTO_INCREMENT
    `parent_id` int unsigned DEFAULT NULL
    `lft` int unsigned NOT NULL DEFAULT 0
    `rgt` int unsigned NOT NULL DEFAULT 0
    ```

  - 非必要欄位

    ```sql
    // 若資料庫有開啟 strict mode，則不能使用 depth 功能 (取資料時，自動計算階層數)，需要在儲存時，給予指定的 level
    `level` int unsigned NOT NULL
    ```

- Model

  ```php
  use Kalnoy\Nestedset\NodeTrait;

  class Category extends Model
  {
      use NodeTrait;

      protected $table = 'category';
      protected $guarded = [];

      /**
       * 對應 lft column
       */
      public function getLftName()
      {
          return 'lft';
      }

      /**
       * 對應 rgt column
       */
      public function getRgtName()
      {
          return 'rgt';
      }
  }
  ```

## 範例

> 底下假設
>
> $maxLevel = 3
>
> A 的 $id = 1，$parentId = null
>
> AA 的 $id = 2，$parentId = 1
>
> AAA 的 $id = 3，$parentId = 2

### 1. 取得同一個 parent id 的分類

```php
$parentId = 2;
echo Category::where('parent_id', $parentId)
    ->defaultOrder()
    ->get();

// result:
[
    [
        'id' => 3,
        'name' => 'AAA',
        'level' => 3,
        ...
    ],
    [
        'id' => 30,
        'name' => 'AAB',
        'level' => 3,
        ...
    ],
    [
        'id' => 300,
        'name' => 'AAC',
        'level' => 3,
        ...
    ]
]
```

### 2. 取祖先跟自己的名稱 (ex: 麵包屑)

```php
$id = 3;
$categories = Category::defaultOrder()->ancestorsAndSelf($id);
echo $categories->count() ? implode(' > ', $categories->pluck('name')->toArray()) : '';

// result:
A > AA > AAA
```

### 3. 取得後代的 tree 直到最大層級

```php
echo Category::where('level', '<=', $maxLevel)
    ->defaultOrder()
    ->get()
    ->toTree();

// result:
[
    [
        'id' => 1,
        'name' => 'A',
        'level' => 1,
        'children' => [
            'id' => 2,
            'name' => 'AA',
            'level' => 2,
            'children' => [
                'id' => 3,
                'name' => 'AAA',
                'level' => 3,
                'children' => [

                ],
            ],
        ],
    ],
    [
        'id' => 10,
        'name' => 'B',
        'level' => 1,
        'children' => [
            'id' => 20,
            'name' => 'BA',
            'level' => 2,
            'children' => [

            ],
        ],
    ],
]
```

### 4. 取得最大階層的分類 (ex: 下拉選單)

```php
echo Category::with(['ancestors'])
    ->where('level', $maxLevel)
    ->defaultOrder()
    ->get()
    ->map(function ($category) {
        if ($category->ancestors->count()) {
            $category->name = implode(' > ', $category->ancestors->pluck('name')->toArray()) . " > {$category->name}";
        }

        return $category;
    });

// result:
[
    [
        'id' => 3,
        'name' => 'A > AA > AAA',
        'level' => 3,
        ...
    ],
    [
        'id' => 30,
        'name' => 'A > AA > AAB',
        'level' => 3,
        ...
    ],
    [
        'id' => 300,
        'name' => 'A > AA > AAC',
        'level' => 3,
        ...
    ]
]
```

### 5. 新增分類

```php
# 新增根節點
Category::create([
    'name' => 'A',
    'level' => 1,
    ...
]);

# 新增子節點
$parentId = 1;
// 先找到父節點
$parentCategory = Category::find($parentId);
// 再新增該父節點的子節點
$parentCategory->children()->create([
    'name' => 'AA',
    'level' => 2,
    ...
]);
```

### 6. 更新分類

```php
$id = 1;
$category = Category::find($id);
$category->update([
    'name' => 'A',
    ...
]);
```

### 7. 刪除分類

```php
$id = 1;
// 刪除前須視情況做檢核，不然會連同子分類一起刪除
Category::find($id)->delete();
```

### 8. 排序同階層分類

```php
$parentId = null;
$parentCategory = Category::find($parentId);
// 排序 A、B、C
$treeData = [
    ['id' => 1],
    ['id' => 10],
    ['id' => 100],
];
Category::rebuildSubtree($parentCategory, $treeData);

// 排序 C、B、A
$treeData = [
    ['id' => 100],
    ['id' => 10],
    ['id' => 1],
];
Category::rebuildSubtree($parentCategory, $treeData);
```

## 參考

- <a href="https://github.com/lazychaser/laravel-nestedset" target="_blank">官方文件</a>
- <a href="https://iter01.com/655063.html" target="_blank">無限級分類之 Laravel-nestedset 擴充套件包的使用</a>
