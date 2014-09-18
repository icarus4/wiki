# Table of Content
[TOC]


# 待看教學文章

- [How I learned to test my Rails applications](http://everydayrails.com/2012/03/12/testing-series-rspec-setup.html)
- [RSpec - iprug-rspec-presentation](http://kerryb.github.io/iprug-rspec-presentation/) by Kerry Buckley
- Better Specs [Chinese](http://betterspecs.org/zh_tw/) / [English](http://betterspecs.org/)
- RSpec 讓你愛上寫測試 by iHower http://www.slideshare.net/ihower/rspec-7394497

# 學習清單
- Mocks 和 Stubs
- 如何建立測試資料 Factory Girl v.s. Fixture
- Capybara
- Continuous Integration
- 常用工具介紹
    - 連續測試 guard
    - shoulda
    - database_cleaner
    - vcr
    - rspec-given
    - simplecov
- ATDD 和 Cucumber


# Tutorial Articles
- Refactor rspec using subject and let
    - http://blog.teamtreehouse.com/an-introduction-to-rspec
    - http://eggsonbread.com/2010/03/28/my-rspec-best-practices-and-tips/
- [Rspec 101](http://www.slideshare.net/jasonjnoble/rspec-101) - 把幾個基本語法快速瀏覽一次
- [RSpec 詳細設定教學](http://everydayrails.com/2012/03/12/testing-series-rspec-setup.html)


# Matcher Notes
- [Match type](https://www.relishapp.com/rspec/rspec-expectations/v/2-0/docs/matchers/type-check-matchers)

# Reference documents
- [Better Specs](http://betterspecs.org/zh_tw/)
- [Matcher](https://www.relishapp.com/rspec/rspec-expectations/v/2-0/docs/matchers)
- API docs http://rubydoc.info/gems/rspec-core/frames
- Relish https://relishapp.com/rspec/rspec-rails/v/2-14/docs
- RSpec **expect** docs
    - https://github.com/rspec/rspec-expectations
    - https://relishapp.com/rspec/rspec-expectations/docs

# Gems for testing
- RSpec
    - RSpec Mocks
        - 用假的物件替換真正的物件，作為測試之用。主要用途有：
        - 無法控制回傳值的外部系統 (例如第三方的網路服務)
        - 建構正確的回傳值很麻煩 (例如得準備很多假資料)
        - 可能很慢，拖慢測試速度 (例如耗時的運算)
        - 有難以預測的回傳值 (例如亂數方法)
        - 還沒開始實作 (特別是採用*TDD*流程)
    - [Shoulda](https://github.com/thoughtbot/shoulda-matchers)
        - 提供了更多Rails的專屬Matchers
    - fuubar
        - 讓輸出更清楚好看
- [Watchr](https://github.com/mynyml/watchr)
    - 是一種Continuous Testing的工具。程式一修改完存檔，自動跑對應的測試。可以大大節省時間，立即回饋。
- [RCov](http://relevance.github.com/rcov/)
    - 用來測試涵蓋度，也就是告訴你哪些程式沒有測試到。有些團隊會追求100%涵蓋率是很好，不過要記得Coverage只是手段，不是測試的目的。
- Faker (for creating random and proper data for database)
- Fabrication (for simple creating instances)
- cucumber
- spork
- autotest
- webrat
- capybara
- CI server
    - CI(Continuous Integration)伺服器的用處是每次有人Commit就會自動執行編譯及測試(Ruby不用編譯，所以主要的用處是跑測試)，並回報結果，如果有人送交的程式搞砸了回歸測試，馬上就有回饋可以知道。以Ruby實作的CI常見有以下選擇：
        - [Bigtuna](http://bigtuna.appelier.com/)
        - [CI Joe](https://github.com/defunkt/cijoe)
        - [Integrity](http://integrityapp.com/)
        - [CruiseControl.rb](http://cruisecontrolrb.thoughtworks.com/)


# RSpec resources
- To start with rspec take a look at this presentation. It contains all the necessary examples: http://kerryb.github.io/iprug-rspec-presentation/#1
- RSpec docs http://relishapp.com/rspec/rspec-rails
- You could watch the following railscasts episodes to have more info about those gems:
    - 155 Beginning with Cucumber
    - 156 Webrat
    - 157 RSpec Matchers & Macros
    - 159 More on Cucumber
