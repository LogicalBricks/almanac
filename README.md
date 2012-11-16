# Almanac
Almanac is the most elegant mountable blog engine that can be easily hooked up in the existing Rails application.

## Main Features
- Slick default design that can be easily customized.
- Markdown for everything.
- Drafts that make sense.
- Easy Google Analytics support.
- Akismet support for spam filtering in comments.
- Built-in social sharing with Facebook and Twitter.
- RSS support.
- Tags for posts.
- Photo uploading.
- Complete integration with Devise and CanCan.
- Tested with RSpec and FactoryGirl
- Uses haml, scss, CoffeeScript and Bootstrap for views.

## Installation
### 1. Add the gem to your `Gemfile`
```ruby
gem "almanac"
```
And run `bundle install`.

### 2. Setup Routes
To hook up Almanac routes to your current Rails app simply put this code in your `config/routes.rd` file

```ruby
mount Almanac::Engine, :at => '/blog'
```

You can obviously setup any route you want. E.g. `/posts` or `/almanac`.

### 3. Run Almanac Migrations
First off, install Almanac migrations:

```ruby
rake almanac:install:migrations
```

Then migrate your database:

```ruby
rake db:migrate
```

### 4. Devise and CanCan Setup
Almanac relies on Devise and CanCan properly configured in your app. In short, the `current_user` variable and CanCan `ability.rb` file has to exist. You can setup permissions for the following Almanac models:

```ruby
can :manage, Almanac::Post
can :manage, Almanac::Blog
can :manage, Almanac::Comment
can :manage, Almanac::Image
```

These particular rules will allow the specified user to do anything with any Almanac record in the database.

### 5. Dragonfly Setup
Almanac relies on the Dragonfly gem for file uploads. Configure Dragonfly in your app by adding the following line to `config/initializers/dragonfly.rb`:

```ruby
require 'dragonfly/rails/images'
```

### 6. Specify User Class Name
Lastly, you'll have to specify the name of your user model. Create a `config/initializers/almanac.rb` file and add the following line there:

```ruby
Almanac.user_class = "User" # other possibilities: "Author", "Writer", etc.
```

## Testing
Almanac's models and controllers are tested with RSpec and FactoryGirl. Rails engines, such as Almanac, are normally tested with a dummy app that is located inside the 'spec' folder. Migrate your test database from the `spec/dummy` directory:

```ruby
rake db:migrate RAILS_ENV=test
```

Go back to the `almanac` directory and run `rspec spec`.

## Contribute
Fork the repo, do work, test it, pull request.