# Rollback
## Example 1
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

## Example 2
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
