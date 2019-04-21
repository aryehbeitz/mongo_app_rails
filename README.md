# Rails with Mongo Db

## setup notes

```
sudo apt-get install -y mongodb
rails new mongo_app –skip-active-record

# add to Gemfile
gem 'mongoid', '~> 6.0'
gem 'bson_ext'

# in `application.rb` remove require 'rails/all'

replace with

require 'rails'

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

%w(
  mongoid
  action_controller/railtie
  action_view/railtie
  action_mailer/railtie
  active_job/railtie
  action_cable/engine
  rails/test_unit/railtie
  sprockets/railtie
).each do |railtie|
  begin
    require railtie
  rescue LoadError
  end
end

# remove config/database.yml and sqlite gem fom Gemfile

grep -r active_record config/ and remove
grep -r active_storage config/ and remove

# run:

rails g mongoid:config

rails g scaffold article name:string content:text

```