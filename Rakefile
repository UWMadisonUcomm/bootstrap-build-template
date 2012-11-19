require 'rubygems'
require 'tempfile'
require 'fileutils'
require 'bundler/setup'
require 'less'
require 'uglifier'

desc "Compile Assets"
task :build do
  # Instantiate the parser, putting our src/less path before src/lib/bootstrap/less in the include path
  parser = Less::Parser.new :paths => [ 'src/less', 'src/lib/bootstrap/less' ], :filename => 'project.less'

  # Parse project.less
  tree = parser.parse( File.open('src/less/project.less').read )

  # Write CSS files, compressed, and un-compressed
  File.open('dist/css/project.css', 'w+') { |f| f.write tree.to_css }
  File.open('dist/css/project.min.css', 'w+') { |f| f.write tree.to_css(:yuicompress => true) }

  # Define the bootstrap JS modules to include ( They have to go in this order )
  bootstrap_js = %w( transition alert button carousel collapse dropdown modal tooltip popover scrollspy tab typeahead affix )

  # Concat all of our javascript into a tempfile
  js = Tempfile.new('js-build')
  bootstrap_js.each { |j| js.write File.open("src/lib/bootstrap/js/bootstrap-#{j}.js").read }

  ## NOTE: ##
  # Add additional javascript here if you'd like
  js.write File.open('src/js/project.js').read

  # Write the uglified version of the javascript
  js.rewind
  File.open('dist/js/project.min.js', 'w+') { |f| f.write Uglifier.compile( js.read ) }
  js.close

  # Copy the tempfile as the non-uglified version of the javascript
  FileUtils.copy js, "dist/js/project.js"

  # Cleanup the temp file
  js.unlink
end

desc "Asset watcher"
task :watch do
  require 'listen'
  # TODO: Add linux watcher lib conditional
  require 'rb-fsevent' if RUBY_PLATFORM.include?('darwin')

  puts "I'm watching you...\n"
  Listen.to(File.expand_path('../src', __FILE__), :filter => /\.(less|js)$/) do
    puts "Building #{Time.now.strftime('%r')}\n"
    begin
      Rake::Task["build"].execute
    rescue Exception => e
      puts e
    end
  end
end
