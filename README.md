[![Build Status](https://travis-ci.com/masaru-tech/lograge_activejob.svg?branch=master)](https://travis-ci.com/masaru-tech/lograge_activejob)

# LogrageActivejob

Add ActiveJobs log for Lograge

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'lograge'
gem 'lograge_activejob'
```

Please remember about [Lograge configuration](https://github.com/roidrage/lograge#installation).

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install lograge_activejob

## Custom setup
### Output file path
You can configure output file path for lograge_activejob. (default is the path set in lograge)

```ruby
# config/initializers/lograge_activejob.rb
Rails.application.configure do
  config.lograge_activejob.logger = ActiveSupport::Logger.new "#{Rails.root}/log/lograge_activejob_#{Rails.env}.log"
end
```

### Additional fields
You can configure additional fields, which will be logged for every exception.

```ruby
# config/initializers/lograge_activejob.rb
Rails.application.configure do
  config.lograge_activejob.custom_options = lambda do |event|
    {
      event_time: event.time.iso8601,
      status: event.payload[:exception_object].blank? ? 200 : 500
    }
  end
end
```

### Ignore jobs
You can mark specific jobs to not be logged.

```ruby
Rails.application.configure do
  config.lograge_activejob.ignore_jobs = ENV.fetch('DISABLE_JOB_LOGS', '').split
end
```


## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/masaru-tech/lograge_activejob. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
