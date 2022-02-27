## join()、leftJoin()、rightJoin()
```
join('contacts', 'users.id', '=', 'contacts.user_id')

join('contacts', function ($join) {
    $join->on('users.id', '=', 'contacts.user_id')
            ->where('contacts.user_id', '>', 5);
})
```

## select()
## addSelect()

## where()
## whereRaw()





## insert()
## insertGetId() 

## update()
## increment()、decrement()
```
increment('votes')
increment('votes', 5)
```


## delete()


# 顯示SQL statement
```
範例1:
DB::enableQueryLog();

// SQL statement

dd(DB::getQueryLog());

範例2:
使用jdorn/sql-formatter套件

DB::enableQueryLog();

// SQL statement

dd(SqlFormatter::format(DB::getQueryLog()[0]['query'], false));
```