# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
directories %w(. libraries resources test spec) \
  .select { |d| Dir.exist?(d) ? d : UI.warning("Directory #{d} does not exist") }

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

# Note: The cmd option is now required due to the increasing number of ways
#       rspec may be run, below are examples of the most common uses.
#  * bundler: 'bundle exec rspec'
#  * bundler binstubs: 'bin/rspec'
#  * spring: 'bin/rspec' (This will use spring if running and you have
#                          installed the spring binstubs per the docs)
#  * zeus: 'zeus rspec' (requires the server to be started separately)
#  * 'just' rspec: 'rspec'

guard :rspec, cmd: 'bundle exec rspec --format documentation' do
  require 'guard/rspec/dsl'
  dsl = Guard::RSpec::Dsl.new(self)

  # Feel free to open issues for suggestions and improvements

  # RSpec files
  rspec = dsl.rspec
  watch(rspec.spec_helper) { rspec.spec_dir }
  watch(rspec.spec_support) { rspec.spec_dir }
  watch(rspec.spec_files)
  watch(%r{^libraries/(.+)\.rb$}) { |m| "spec/unit/libraries/#{m[1]}_spec.rb" }
  watch(%r{^libraries/chef_f5.rb$}) { |m| "spec/unit/recipes/test_create_disabled_nodes_spec.rb" }
  watch(%r{^resources/pool.rb$}) { |m| "spec/unit/recipes/test_create_pool_spec.rb" }
  watch(%r{^resources/pool.rb$}) { |m| "spec/unit/recipes/test_create_disabled_nodes_spec.rb" }
  watch(%r{^test/fixtures/cookbooks/f5_test/recipes/(.+)\.rb$})   { |m| "spec/unit/recipes/#{m[1]}_spec.rb" }

  # Ruby files
  ruby = dsl.ruby
  dsl.watch_spec_files_for(ruby.lib_files)
end
