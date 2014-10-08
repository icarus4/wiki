## Using self-referential association to model friendship
- Railscast: [#163 Self-Referential Association](http://railscasts.com/episodes/163-self-referential-association)



## Using CanCan to build up multi-role scenario ([link](http://stackoverflow.com/questions/21211276/how-to-use-cancan-with-role-model))
- User model
```ruby
class User < ActiveRecord::Base
  has_many :user_roles
  has_many :roles, :through => :user_roles

  # user model has for example following attributes:
  # username, email, password, ...
end

class Role < ActiveRecord::Base
  has_many :user_roles
  has_many :users, :through => :user_roles

  # role model has for example following attributes:
  # name (e.g. Role.first.name => "admin" or "editor" or "whatever"
end

class UserRole < ActiveRecord::Base
  belongs_to :user
  belongs_to :role
end
```

- Extend user model with few helper method
```ruby
class User < ActiveRecord::Base

  def is_admin?
    is_type?("admin")
  end

  def is_editor?
    is_type?("editor")
  end

  def is_whatever?
    is_type?("whatever")
  end

  private

  def is_type? type
    self.roles.map(&:name).include?(type) ? true : false # will return true if the param type is included in the user´s role´s names.
  end

end
```

- Extend ability class
```ruby
class Ability
  include CanCan::Ability

  def initialize(user)
    if user
      can :manage, :all if user.is_admin?
      can :create, Project if user.is_editor?
      can :read, Project if user.is_whatever?
      # .. and so on..
      # you can work with your different roles on base of the given user instance.
    end
  end
end
```
