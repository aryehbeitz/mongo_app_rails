# Rails with Mongo Db

## to begin

```
rvm use 2.5.1
bundle install
rails s
```

navigate to [localhost:3000/articles](http://localhost:3000/articles) to see the magic

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

please note what this command will do ;)

invoke  mongoid
create    app/models/article.rb
invoke    test_unit
create      test/models/article_test.rb
create      test/fixtures/articles.yml
invoke  resource_route
 route    resources :articles
invoke  scaffold_controller
create    app/controllers/articles_controller.rb
invoke    erb
create      app/views/articles
create      app/views/articles/index.html.erb
create      app/views/articles/edit.html.erb
create      app/views/articles/show.html.erb
create      app/views/articles/new.html.erb
create      app/views/articles/_form.html.erb
invoke    test_unit
create      test/controllers/articles_controller_test.rb
create      test/system/articles_test.rb
invoke    helper
create      app/helpers/articles_helper.rb
invoke      test_unit
invoke    jbuilder
create      app/views/articles/index.json.jbuilder
create      app/views/articles/show.json.jbuilder
create      app/views/articles/_article.json.jbuilder
invoke  assets
invoke    coffee
create      app/assets/javascripts/articles.coffee
invoke    scss
create      app/assets/stylesheets/articles.scss
invoke  scss
create    app/assets/stylesheets/scaffolds.scss


```