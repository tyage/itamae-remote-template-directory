# Itamae::Plugin::Resource::RemoteTemplateDirectory

Extended remote_directory resource which each local file is template.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'itamae-plugin-resource-remote_template_directory'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install itamae-plugin-resource-remote_template_directory

## Usage

Basic actions and attributes are same as [remote_directory resource](https://github.com/itamae-kitchen/itamae/wiki/remote_directory-resource).
Also, `variables` attribute of [template resource](https://github.com/itamae-kitchen/itamae/wiki/template-resource) is available.

Here is sample recipe and its result.

`recipe.rb`

```rb
node.reverse_merge!(
  var: 'value of node var'
)

remote_template_directory 'copy directory' do
  source 'nginx-confs'
  path '/etc/nginx/sites-enabled'
  variables(
    var1: 'value of var1',
    var2: 'value of var2'
  )
end
```

`nginx-confs/test.conf`

```rb
here is template
<%= @var1 %>
<%= @var2 %>
<%= node[:var] %>
```

`/etc/nginx/sites-enabled/test.conf`

```
here is template
value of var1
value of var2
value of node var
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake true` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/itamae-plugin-resource-remote_template_directory.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
