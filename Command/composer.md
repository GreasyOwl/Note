# Composer指令

## 檢視全域套件安裝路徑
```
> composer config --global --list

路徑在 [home] = your-path
```

## 重新產生autoload_classmap內容
```
> composer dump-autoload

# 官方建議在正式環境執行底下指令，來優化自動加載速度
> composer dump-autoload --optimize
```
參考:
* [官方文件](https://getcomposer.org/doc/articles/autoloader-optimization.md)
* [芥龍 【成為 Modern PHPer】](https://ithelp.ithome.com.tw/articles/10214905 "Composer的小技巧 > 增加 autoload 效率 > 基礎優化")
