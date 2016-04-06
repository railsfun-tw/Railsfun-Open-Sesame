# 1. {irb} 開宗明義
## 所有的東西都是物件
不像 Java 程式語言有基本資料類型(primitive data type)(Int/Float/...)，**Ruby 程式語言中所有的東西都是物件**，包含看似比較特殊的 Nil/True/False 也一樣。

### class()、methods() 方法
在所有 Ruby 類別(class)中有一些方法(method)是共有的，像是 `class` 跟 `methods` 這兩個方法。

`class` 方法會回傳該物件的類別：

```ruby
 > 123.class()
 => Fixnum 
 > 123.123.class()
 => Float
 > true.class()
 => TrueClass
 > nil.class()
 => NilClass 
 # 任何東西都可以這樣用
```

`methods` 方法會回傳包含該物件類別的所有方法的陣列：

```ruby
 > 0.9.methods()
 => [:to_s, :inspect, :coerce, :-@, :+, :-, :*, :/, :quo, :fdiv, :%, :modulo, :divmod, :**, :==, :===, :<=>, :>, :>=, :<, :<=, :eql?, （中間省略）, :respond_to?, :extend, :display, :method, :public_method, :singleton_method, :define_singleton_method, :object_id, :to_enum, :enum_for, :equal?, :!, :!=, :instance_eval, :instance_exec, :__send__, :__id__]
```

若使用 Awesome Print 來輸出 `methods()` 方法回傳的內容的話還可以知道該方法的定義域：

```ruby
 > require("awesome_print")
 => true 
 > ap(nil.methods())
[
    [ 0]                          !()                 NilClass (BasicObject)
    [ 1]                         !=(arg1)             NilClass (BasicObject)
    [ 2]                         !~(arg1)             NilClass (Kernel)
    [ 3]                          &(arg1)             NilClass
    [ 4]                        <=>(arg1)             NilClass (Kernel)
    [ 5]                         ==(arg1)             NilClass (BasicObject)
    [ 6]                        ===(arg1)             NilClass (Kernel)
    [ 7]                         =~(arg1)             NilClass (Kernel)
    [ 8]                          ^(arg1)             NilClass
    [ 9]                     __id__()                 NilClass (BasicObject)
    [10]                   __send__(*arg1)            NilClass (BasicObject)
　　　　　（……中間省略……）
    [56]                       to_a()                 NilClass
    [57]                       to_c()                 NilClass
    [58]                    to_enum(*arg1)            NilClass (Kernel)
    [59]                       to_f()                 NilClass
    [60]                       to_h()                 NilClass
    [61]                       to_i()                 NilClass
    [62]                       to_r()                 NilClass
    [63]                       to_s()                 NilClass
    [64]                      trust()                 NilClass (Kernel)
    [65]                    untaint()                 NilClass (Kernel)
    [66]                    untrust()                 NilClass (Kernel)
    [67]                 untrusted?()                 NilClass (Kernel)
    [68]                          |(arg1)             NilClass
]
 => nil
```

取名為 `to_*()` 方法為兩類別間轉換之用。

## 程式庫分類
Ruby 的程式庫分為三類：

### Core（核心）（官方）
Core 程式庫中的所有類別於初始狀態就可以直接調用。

### Std-lib（標準程式庫）（官方）
Std-lib 中的類別需要額外的 `require` 呼叫引入才可以存取。

### Gem（直譯：寶石）
Gems 為**第三方**所設計的程式庫，需要手動使用 `gem` 命令來安裝，然後再於程式中 `require` 才可以存取。

您可以自 [The Ruby Toolbox](https://www.ruby-toolbox.com/) 網站找到各種不同用途下可用的 Gem 程式庫

![The Ruby Toolbox 網頁截圖](Resources/Pictures/The%20Ruby%20Toolbox%20pageshot.png)

## 如何尋求幫助
### 查詢參考文件
#### 標準程式庫
您可以於  [Ruby-Doc.org](http://ruby-doc.org/) 查詢所有 Ruby 官方的 Core、Std-lib 程式庫的應用程式介面(API)參考資料。
![Ruby-Doc.org screenshot](Resources/Pictures/Ruby-Doc.org%20screenshot.png)

#### Gem
Gem 的參考文件請參考該 Gem 的官方網站，大部份都會寫在該 GEM 的 README 文件中。

如果 Gem 被托管在 GitHub 程式碼托管網站上，您還可以察看它的 Wiki。

##### 建檔軟體缺陷報告／議題<br />File bug report/issue
如果您發現 Gem 有軟體缺陷(bug)或是有其他問題而且 Gem 托管於 GitHub 服務上您可以到該程式庫的軟體缺陷／議題追蹤系統(bug/issue tracker)建檔一個軟體缺陷報告／議題。

![議題追蹤系統範例圖片](Resources/Pictures/Issue%20tracker%20example01.png)

##### 建立變更拉取請求(pull request)
若您修改了 Gem 來源碼並想將您的變更送回上游專案而且 Gem 托管於 GitHub 服務上您可以建立一個變更拉取請求(pull request)


## 基本類別介紹
### Fixnum 類別－一般整數
此類別為一般的整數，可以作基本的數值運算

```ruby
 > 123
 => 123
 > 123 + 123
 => 246
 > 123 / 123
 => 1
```

### Bignum 類別－大數
Ruby 可以作大數運算，當數值變得太大時 Ruby 會轉換類別至 Bignum。

```ruby
 >  123.class
 => Fixnum
 > 123 ** 123
 => 114374367934617190099880295228066276746218078451850229775887975052369504785666896446606568365201542169649974727730628842345343196581134895919942820874449837212099476648958359023796078549041949007807220625356526926729664064846685758382803707100766740220839267
 > (123 ** 123).class
 => Bignum 
```

### Float 類別－浮點數
Float 類別為浮點數，Ruby 的程式語言與Ｃ一樣會有精確度造成的「整數運算結果會帶額外小數」的問題，您可以用 `round()` 方法來解決這個問題

```ruby
（範例待補）
```

### Array 類別－陣列
跟原生程式語言不同，Ruby 中的陣列為不定長度，不需要事先宣告大小。

#### 標示法
##### 單維度陣列
```ruby
 > ap([0, 1, 2, 3])
[
    [0] 0,
    [1] 1,
    [2] 2,
    [3] 3
]
 => nil 
```

##### 多維度陣列
```ruby
 > ap([[00, 01, 02, 03], [10, 11, 12, 13], [20, 21, 22, 23], [30, 31, 32, 33]])
[
    [0] [
        [0] 0,
        [1] 1,
        [2] 2,
        [3] 3
    ],
    [1] [
        [0] 10,
        [1] 11,
        [2] 12,
        [3] 13
    ],
    [2] [
        [0] 20,
        [1] 21,
        [2] 22,
        [3] 23
    ],
    [3] [
        [0] 30,
        [1] 31,
        [2] 32,
        [3] 33
    ]
]
 => nil
 > [[00, 01, 02, 03], [10, 11, 12, 13], [20, 21, 22, 23], [30, 31, 32, 33]][2][2]
 => 22
```

### String 類別－字元串列
#### 標示法
##### *REPLACE ME*
```ruby
 > "Hello kitty!"
 => "Hello kitty!"
```

Ruby 支援中文（以及其他語言文字）組成的字串：

```ruby
> "許蓋功"
=> "許蓋功"
> "許蓋功213213"
=> "許蓋功213213"
```

### NilClass 類別－nil
`nil` 是一個特殊的物件，用來代表「空」 

### TrueClass、FalseClass 類別－true、false
true、false 物件用來就行布林(boolean)運算：


在 Ruby 的布林運算中**只有 `nil` 和 `false` 會被解釋為「假(false)」**，其他類別與數值（包含 `0`）皆會解釋為「真(true)」

```ruby
 > nil && false && 0
 => 0
```

```ruby
 > true || true || false
 => true
 > false || false || true
 => true
 > nil || nil || 1
 => 1
 > 1 && 2 && 3
 => 3
```


```ruby
String 的 ” 與 ’ 的分別，還有 “#{xxx}” 的用法
“MMM#{1+1}MMM” #=> “MMM2MMM”
‘NNN#{2+2}NNN’ #=> “NNN\#{2+2}NNN”

Hash (Symbol{object_id}) & 新舊兩種宣告方式
{:wer => 123 , :sdf => 234} #=> {:wer => 123 , :sdf => 234}
{wer:123 , sdf: 234} #=> {:wer => 123 , :sdf => 234}
#字元和冒號不能空白，後面數值可以

全世界只有兩種東西為非：Nil, False
nil && false && 0 #=> 0

結構：if-else / unless-else / case-when / each …
puts 123 unless false if true unless nil if 1

後置判斷式，三元判斷式

```
