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