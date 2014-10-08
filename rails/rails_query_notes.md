## Multi-level association query
- If the association is as follows:
```ruby
class Country < ActiveRecord::Base
  has_many :states
end

class State < ActiveRecord::Base
  belongs_to :country
  has_many :cities
end

class City < ActiveRecord::Base
  belongs_to :state
  has_many :people
end

class Person < ActiveRecord::Base
  belongs_to :city
end
```

- To query all people of the first city:
```ruby
People.joins(:city => {:state => :country})
      .where(:country => {:id => Country.first.id}).all
```
