# Strano
- [Strano](http://thechangelog.com/strano-github-powered-web-ui-for-capistrano-deployment/) ([Github](https://github.com/joelmoss/strano)) - web UI for Capistrano deployment

# Samson
- [samson](https://github.com/zendesk/samson) - Web interface for deployments

### View the current status of all your projects:
![](https://camo.githubusercontent.com/8224187a9a942295e452b572e3c76eb954c13fb3/687474703a2f2f662e636c2e6c792f6974656d732f336e3066306d336a325132343259316b3331314f2f53616d736f6e2e706e67)

### Allow anyone to watch deploys as they happen:
![](https://camo.githubusercontent.com/b980d661b9299942219fc4ffb7aea2b903fb09eb/687474703a2f2f636c2e6c792f696d6167652f316d3051316b3272314d33322f4d61737465725f6465706c6f795f5f7375636365656465645f2e706e67)

### View all recent deploys across all projects:
![](https://camo.githubusercontent.com/d3f5942d9ee35e72c8ab5628465e00d9b858f205/687474703a2f2f636c2e6c792f696d6167652f3237306c31653373326531702f53616d736f6e2e706e67)

# Webistrano

# Mina
## Rollback Example 1
```ruby
desc "Rolls back the latest release"
task :rollback => :environment do
  queue! %[echo "-----> Rolling back to previous release for instance: #{domain}"]

  # Delete existing sym link and create a new symlink pointing to the previous release
  queue %[echo -n "-----> Creating new symlink from the previous release: "]
  queue "echo `cat #{deploy_to}/last_version` | ruby -e 'p gets.to_i-1'"
  queue! "echo `cat #{deploy_to}/last_version` | ruby -e 'p gets.to_i-1' | xargs -I active ln -nfs '#{deploy_to}/releases/active' '#{deploy_to}/current'"

  # Remove latest release folder (active release)
  queue %[echo -n "-----> Deleting active release: "]
  queue "echo `cat #{deploy_to}/last_version`"
  queue! "echo `cat #{deploy_to}/last_version` | xargs -I active rm -rf #{deploy_to}/releases/active"

  # Update the "last_version" file
  queue %[echo -n "-----> Updating last_version file. "]
  queue! "mv #{deploy_to}/last_version #{deploy_to}/del_version"
  queue! "echo `cat #{deploy_to}/del_version` | ruby -e 'p gets.to_i-1' > #{deploy_to}/last_version"
  queue! "rm #{deploy_to}/del_version"

end
```

## Rollback Example 2
```ruby
desc "Rolls back the latest release"
task :rollback => :environment do
  queue! %[echo "-----> Rolling back to previous release for instance: #{domain}"]

  # Delete existing sym link and create a new symlink pointing to the previous release
  queue %[echo -n "-----> Creating new symlink from the previous release: "]
  queue %[ls "#{deploy_to}/releases" -Art | sort | tail -n 2 | head -n 1]
  queue! %[ls -Art "#{deploy_to}/releases" | sort | tail -n 2 | head -n 1 | xargs -I active ln -nfs "#{deploy_to}/releases/active" "#{deploy_to}/current"]

  # Remove latest release folder (active release)
  queue %[echo -n "-----> Deleting active release: "]
  queue %[ls "#{deploy_to}/releases" -Art | sort | tail -n 1]
  queue! %[ls "#{deploy_to}/releases" -Art | sort | tail -n 1 | xargs -I active rm -rf "#{deploy_to}/releases/active"]
end
```
