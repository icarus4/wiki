# Custom libraries and class files path

custom lib、class 放置於 lib/，並於設定如下

```ruby
# application.rb
config.autoload_paths += Dir["#{config.root}/lib/**/"]
```
