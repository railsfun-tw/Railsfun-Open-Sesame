# 0. 準備環境
## 你***不應該***使用 Microsoft Windows 作業系統寫 Ruby 程式
### 理由
  * 很多 Ruby 的程式庫都只相容 GNU/Linux 作業系統（而且有的還需要建構原生(native)語言(C...)的程式），於 Windows 上要使用這些程式庫是比較困難的。
  * 效能較差

## 安裝 Ruby Version Manager (RVM)（本教材僅支援此安裝方式安裝的 Ruby）
雖然說安裝 Ruby 有很多種方式，不過使用 [Ruby Version Manager (RVM)](https://rvm.io/)  來安裝 Ruby（以及之後會用到的 Rails）有下列好處：

* 可以選擇想要安裝的版本
* （待補）

安裝方式請參考官方網站教學，安裝完後您需要登出再登入 RVM 安裝上去的環境變數才會生效，我們才可以直接於終端機中直接執行 `rvm` 命令。

## 透過 RVM 安裝 Ruby
### 1. 確認 RVM 可用的 Ruby 版本
執行 `$ rvm list known` 命令可以列出所有 RVM 支援的 Ruby 版本，您會發現 Ruby 有非常多不同的實作，其中 Matz's Ruby Interpreter(MRI Ruby) 為 Ruby 程式語言創作者松本行弘(Yukihiro “Matz” Matsumoto)所開發，於本教學中我們將會使用此 Ruby 實作。

```bash
$ rvm list known
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p643]
[ruby-]2.1.4
[ruby-]2.1[.5]
[ruby-]2.2[.1] # 最新釋出版本
[ruby-]2.2-head # 尚未釋出的開發中版本
ruby-head

（下方省略）
```

**注意：**`rvm list known` 命令中列出的最新版本未必是上游的最新版本。MRI 版最新的版本請參考 [Ruby 官方網站下載頁面](https://www.ruby-lang.org/zh_tw/downloads/) 的說明。

#### 參考資料<br />Reference Data
* [RVM: Ruby Version Manager - './install' - Installing RVM.](https://rvm.io/rubies/installing)
* [關於 Ruby](https://www.ruby-lang.org/zh_tw/about/)
* [Ruby MRI - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Ruby_MRI)

### 2. 安裝 Ruby
執行 `$ rvm install 〈Ruby 版本〉` 來安裝指定的 Ruby 版本。

RVM 會試著找有沒有已建構好了軟體，若沒有的話將會下載該版本的 Ruby 來源程式碼(source code)，建構好 Ruby 之後將其安裝到家目錄底下的 `.rvm/bin` 目錄中，如果建構 Ruby 需要的軟體尚未安裝的話會跟您提示輸入您的密碼將這些軟體先安裝到系統中。

### 3. 確認目前作用中的 Ruby 版本是你安裝的版本
* 執行 `$ ruby --version` 來察看目前作用中的 Ruby 版本。
* 執行 `$ which ruby` 來察看 `ruby` 命令會執行的可執行檔(executable)路徑，如果路徑是 `/usr/.../bin/ruby` 代表這是系統所安裝的 Ruby 而**不是** RVM 安裝的 Ruby，正確的路徑應為 `〈家目錄〉/.rvm/rubies/ruby-〈Ruby 版本〉/bin/ruby`。

安裝完 Ruby 之後您應可以存取 `ruby`、`irb`、`gem` 等命令，如果沒有的話請再次檢查您的 Ruby 安裝是否正確無誤。

## Interactive RuBy(IRB) 使用簡介
Interactive RuBy(IRB) 為 Ruby 自帶的互動式環境，於 IRB 中您可以在裏面一行一行執行 Ruby 語言的語句並觀察它運行的結果，IRB 會將輸出的訊息印出來（如果有）並印出回傳值，很適合拿來學習 Ruby。

```ruby
$ irb
irb(main):001:0> puts "Hello world"
Hello World
=> nil # 回傳值為 nil
irb(main):002:0> quit # 執行 quit 結束 IRB
$ # irb 結束，回到原來的 shell 環境
```

### 參考資料
* [Ruby in Twenty Minutes](https://www.ruby-lang.org/en/documentation/quickstart/)
* [Module: IRB (Ruby 2.0.0)](http://ruby-doc.org/stdlib-2.0.0/libdoc/irb/rdoc/IRB.html)

## 安裝 Awesome Print（建議）
[Awesome Print](https://github.com/michaeldv/awesome_print) 是一個可以將 Ruby 物件用美觀的方式印出的第三方程式庫，安裝完後於程式中執行 `require "awesome_print"` 即可以用 `ap()` 來取代 `puts()` 或 `pp()` 方法(method)印出任何的 Ruby 物件。

`````ruby
irb> puts([1, 3, 2, [2, 3]])
1
3
2
2
3
 => nil 

irb> pp([1, 3, 2, [2, 3]])
[1, 3, 2, [2, 3]]
=> [1, 3, 2, [2, 3]]

irb> ap([1, 3, 2, [2, 3]])
[
    [0] 1,
    [1] 3,
    [2] 2,
    [3] [
        [0] 2,
        [1] 3
    ]
]
 => nil 
`````

執行下列命令即可安裝 Awesome Print：
`````
? gem install awesome_print
`````
