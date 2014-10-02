# Gem
## Bug tracking
- [Airbrake](https://airbrake.io/) ([github](https://github.com/airbrake/airbrake))

# Model
## Polymorphic Association
- [Polymophic association](http://railscasts.com/episodes/154-polymorphic-association)
  - 單一 controller 處理多種情況的 comments。Ex: Article 有 comments，Photo 也有 comments，如何一份 code 就同時做到兩種 comments 的 CRUD
  - 注意可用 `classify` / `constantize` 來簡化處理
```ruby
def find_commentable
  params.each do |name, value|
    if name =~ /(.+)_id$/
      return $1.classify.constantize.find(value)
    end
  end
  nil
end
```

## serialize
- 在 text 欄位塞入 Hash / JSON / Array string 時可用
  - Reference: [[Rails] Serialize 用法](http://wildjcrt.pixnet.net/blog/post/29101760-%5Brails%5D-serialize-%E7%94%A8%E6%B3%95)
