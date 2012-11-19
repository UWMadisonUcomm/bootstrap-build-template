# A sample Gemfile
source "https://rubygems.org"

gem 'rake'
gem 'therubyracer'
gem 'less'
gem "uglifier", "~> 1.3.0"
gem 'listen'

# Check for platform specific listener helpers
if RUBY_PLATFORM.include?('darwin')
  gem 'rb-fsevent'
elsif RUBY_PLATFORM.include?('linux')
  gem 'rb-inotify'
end
