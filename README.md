# Rolling

Rolling is a minimalist gem the handle scoped role without any dependency.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'rolling'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rolling

## Usage

```ruby
 class User
  include Rolling.new(:admin, :user, :moderator).scope(Forum)
  include Rolling.new(:admin).scope(:backend)
  include Rolling.new(:user)
 end
```

```ruby
  user = User.new
  user.roles[Forum] << :admin
  user.roles.is_admin? #=> false
  user.roles[Forum].is_admin? #=> true
  user.roles << :user
  user.roles.is_user? #=> true
  user.roles[Forum].is_user? # => true
  user.roles[Forum].is?(:user, :admin) #=> true - yes, this is a and
  user.roles[Forum].has?(:user, :moderator) #=> true - yes, this is a or.
```

## Contributing

1. Fork it ( https://github.com/[my-github-username]/rolling/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
