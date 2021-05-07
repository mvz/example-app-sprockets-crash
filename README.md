# README

This example app demonstrates a crash in sprockets + sassc when precompiling assets.

The ingredients to trigger the crash are:

- sprockets 4.0
- administrate 0.15.0 or 0.16.0
- bootstrap-sass

Given these dependencies, adding a scss file (in this repo, `base.scss`) with
the following lines makes running `bundle exec assets:precomile` segfault:

```scss
@import "bootstrap-sprockets";
@import "bootstrap";
```

Adding the following to `config.application.rb` makes the problem go away:

```ruby
config.assets.configure do |env|
  env.export_concurrent = false
end
```

Related bug report: https://github.com/rails/sprockets/issues/706
