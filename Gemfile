# A sample Gemfile
source "https://rubygems.org"

gem 'rake'
gem 'therubyracer'
gem 'less'
gem "uglifier", "~> 1.3.0"
gem 'listen'

# If we're on a mac use rb-fsevent for listening
# TODO: Add linux watcher lib conditional
if RUBY_PLATFORM.include?('darwin')
  gem 'rb-fsevent'
end
