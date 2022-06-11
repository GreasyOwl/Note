# 顯示資料
## {{ $data }}
```
相等於 <?= htmlspecialchars($data) ?>
防止XSS攻擊
```
## {!! $data !!}
```
相等於 <?= $data ?>
未防止XSS攻擊
常用於輸出html內容
```
# Blade與JavaScript框架
## @{{ data }}
```
相等於 <?= {{ data }} ?>
Blade指令前加@，用來避免被Blade解析
在Vue框架中，用於顯示變數資料
```
## Render JSON
```
<script>
    var app = @json($array);

    // Laravel 8.70
    var app = {{ Js::from($array) }};
</script>
```
# Blade指令
## 條件
```
@if ()

@elseif ()

@else

@endif
```
```
@unless ()

@endunless

@if的相反語法，@unless ($hasPaid) 相等於 @if (!$hasPaid)
```
## 迴圈
```
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor
 
@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach
 
@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse
 
@while (true)
    <p>I'm looping forever.</p>
@endwhile
```
## $loop變數
```
用於foreach、forelse之中

// 目前項目的索引 (從0開始)
$loop->index

// 目前項目的索引 (從1開始)
$loop->iteration

// 還剩下多少個項目
$loop->remaining

// 項目總數
$loop->count

// 判斷是否為第一個項目
$loop->first

// 判斷是否為最後一個項目
$loop->last

// 判斷是否為偶數的項目
$loop->even

// 判斷是否為奇數的項目
$loop->odd

// 巢狀迴圈中，目前迴圈的層數
$loop->depth

// 巢狀迴圈中，父層迴圈的$loop變數
$loop->parent

// 範例
@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif
 
    @if ($loop->last)
        This is the last iteration.
    @endif

    <p>{{ $loop->iteration }}: {{ $user->name }}</p>

    @foreach ($user->posts as $post)
        @if ($loop->parent->first)
            This is the first iteration of the parent loop.
        @endif

        <p>{{ $loop->parent->iteration }}.{{ $loop->iteration }}: {{ $post->title }}</p>
    @endforeach
@endforeach
```
## 模板繼承
```
// layouts/master.blade.php (父blade)
@yield('title', 'default title')

@yield('content')

@section('js')
    <script src="app.js"></script>
@show
```
```
// product.blade.php (子blade)
@extends('layouts.master')

@section('title', '商品')

@section('content')
    <ul>
        @each('list', $products, $product, 'empty-list')
    </ul>

    @include('success-button', ['text' => '儲存'])
@endsection

@section('js')
    @parent

    <script src="product.js"></script>
@endsection
```
```
// success-button.blade.php
<button type="button">{{ $text }}</button>
```
```
// list.blade.php
<li>
    {{ $product->name }}
</li>
```
```
// empty-list.blade.php
<li>
    沒有商品
</li>
```
## 全域共用變數
```
// App\Providers\ViewServiceProvider
public function boot()
{
    // 方法一
    view()->share('posts', Post::get());

    // 方法二
    view()->composer([
        'includes.header', 
        'includes.footer'
    ], function ($view) {
        $view->with('posts', Post::get());
    });

    // 方法三
    view()->composer('includes.*', PostComposer::class);
}
```
```
// App\Http\ViewComposers\PostComposer
<?php
namespace App\Http\ViewComposers;

use App\Models\Post;
use Illuminate\View\View;

class PostComposer
{
    private $post;

    public function __construct(Post $post)
    {
        $this->post = $post;
    }

    public function compose(View $view)
    {
        $view->with('posts', $this->post->get());
    }
}
```
## 自訂Blade指令
```
// App\Providers\BladeServiceProvider
use Illuminate\Support\Facades\Blade;

public function boot()
{
    Blade::directive('ifOdd', function ($expression) {
        return "<?php if ($expression % 2 != 0): ?>";
    });

    Blade::directive('newlinesToBr', function ($expression) {
        return "<?php echo nl2br({$expression}); ?>";
    });
}
```
```
// test.blade.php
@ifOdd (5)
@else
@endif

@newlinesToBr($remark)
```