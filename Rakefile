require 'rubygems'
require 'bundler/setup'
require 'less'

desc "Compile Assets"
task :build do
  # Instantiate the parser, putting our src/less path before src/lib/bootstrap/less in the include path
  parser = Less::Parser.new :paths => [ 'src/less', 'src/lib/bootstrap/less' ], :filename => 'project.less'

  # Parse project.less
  tree = parser.parse( File.open('src/less/project.less').read )

  # Write CSS files, compressed, and un-compressed
  File.open('dist/css/project.css', 'w+') { |f| f.write tree.to_css }
  File.open('dist/css/project.min.css', 'w+') { |f| f.write tree.to_css(:yuicompress => true) }
end


desc "Asset watcher"
task :watch do
  require 'listen'
  # TODO: Add linux watcher lib conditional
  require 'rb-fsevent' if RUBY_PLATFORM.include?('darwin')

  puts "I'm watching you...\n"
  Listen.to(File.expand_path('../src', __FILE__), :filter => /\.less$/) do
    puts "Building #{Time.now.strftime('%r')}\n"
    Rake::Task["build"].execute
  end
end
