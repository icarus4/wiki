# 參考資料
- [關於ruby語言 與Rails框架](http://diyland.biz/?opt=detail&topic=16&id=19601)
- [[翻譯] 是什麼造就了好的軟體工程文化？(下)](http://blog.littlelin.info/posts/2014/09/21/what-makes-good-engineering-culture-2)

# 報告架構
## 舉 Instagram 為例子 ([stack 介紹](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances-dozens-of))
- 3 develeper to serve 14 million+ users (2012) in a little over a year. (200 million now)
- using django (a Rails clone)

# Pain of developer
- 文件不齊
- framework 停止維護
- debug 工具不足，難以debug
- 市佔率不夠高，有問題解答不好找
- 遇到問題找不到可以信賴的 library 來解決
- 改變 library 版本很麻煩
- 寫個功能寫好久，結果需求改變做白工
- 多人同步開發，database schema 同步問題難以解決
- 測試難寫難維護，搞得沒人想寫測試 <-- 做產品不寫測試，等 code base 一大，什麼問題都會出現
- 應徵進來的 developer 水準良莠不齊
- 安全機制沒做好，網站充滿漏洞
- query 難寫難maintain，換了database時query還要重寫
- join table好用又有彈性，但join table query很麻煩


# What is Rails?

## 抄襲就是最好的致敬
- there are hundrens of rails-like web framework

# Why Rails?

## 最熱門的 web framework
- 線上coding教學平台基本上只教兩種 web 技術：Rails & Node.js


## 高效率
- 集中精力專注在真正重要的事情上
  - 投資牆超過三千行的 code，用 Rails 只需要 150~300 行以內搞定
  - 大量節省下來的開發時間，可以趁開發者還記憶猶新時拿來寫測試
  - 開發者有多餘的時間研究更 cutting edge 的技術，成員們不斷成長之下對公司而言才是好事

### Reasons
- Ruby
  - 2006年為TIOBE獲選為年度程式語言
  - 示範 big number 運算
- Database query, validation 好寫易讀好維護
  - Model association
- Gem system
- Tooooooo many excellent gems
  - better errors
  - devise, omniauth

## 好維護
- 先進漂亮的framework架構
- 預設做法即可確保高安全性（不用擔心SQL injection）
- 最重視測試的社群
  - 完整、語意化的測試寫法，甚至測試程式碼可直接輸出成 spec 文件
- 寫的程式碼少，代表 bug 少、trace快
- 寫的程式碼少，一旦需要增減新功能時，不再是痛苦，就算原先架構設計不良，要砍掉重做也很快

## easy debug
- easy to see DB query result and cost time

## 活躍的社群
- 官方開發能量高，不斷納入好東西
- 支援度高，非常多人一起維護熱門套件

## 省錢
- 找一個人給兩份薪水做三個人的事情
- 一般而言程度相近的 rails developer vs PHP developer，rails developer生產力約為三倍
- 一個 Gary 寫 rails 等於 5 Gary 個寫 PHP 的戰力


## 安全
- 未來要做交易功能，安全非常重要

# Rails vs PHP
- ActiveRecord 比較

# Rails vs Laravel
## Popular?
- http://www.quora.com/PHP-Frameworks/Why-should-someone-use-rails-over-laravel
- search google "site:github.com ruby on rails" vs "site:github.com laravel"
- search google "site:github.com ruby" vs "site:github.com php"
- search google "site:stackoverflow.com rails" vs "site:github.com laravel"

## History
- Laravel: Initial release  February 22, 2012
  - too young

## Documentation

# 現有架構缺陷
- database 規劃
- 變數、function 命名不佳

# Real-time with Faye
- [High performance Publish/Subscribe solution for Ruby On Rails or Juggernaut vs. Faye](http://rails-alex.blogspot.tw/2011/10/high-performance-publishsubscribe.html)
  - 30000 request per minute and 6000+ connection to Faye
  - About 90% of requests do pushes to Faye
