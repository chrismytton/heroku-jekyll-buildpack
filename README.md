# heroku-jekyll-buildpack

This buildpack compiles your Jekyll site when you push it to Heroku. Use it with [rack-jekyll](https://github.com/adaoraul/rack-jekyll) to serve your Jekyll application from Heroku without having to wait for the `_site` directory to be build each time the application boots.

## Usage

This buildpack works best with [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) so that it can be used with your app's existing buildpacks.

## Example

#### .buildpacks

    https://github.com/heroku/heroku-buildpack-ruby
    https://github.com/chrismytton/heroku-jekyll-buildpack

#### config.ru

```ruby
require 'rack/jekyll'
Jekyll::PluginManager.require_from_bundler
run Rack::Jekyll.new
```

#### Gemfile

```ruby
source 'https://rubygems.org'
gem 'jekyll'
gem 'rack-jekyll'
```

#### Procfile

    web: bundle exec rackup -p $PORT

### New Heroku app

    $ heroku create jekyll-site --buildpack https://github.com/ddollar/heroku-buildpack-multi

### Existing Heroku app

    $ heroku buildpacks:set https://github.com/ddollar/heroku-buildpack-multi.git
