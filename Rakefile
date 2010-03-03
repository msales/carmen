require 'rubygems'
require 'rake'
require 'hanna/rdoctask'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "carmen"
    gem.summary = %Q{A collection of geographis country and state names for Ruby}
    gem.description = %q{A collection of geographis country and state names for Ruby. Also includes replacements for Rails' country_select and state_select plugins.}
    gem.email = %q{max@jungeelite.de}
    gem.homepage = %q{http://github.com/namxam/carmen}
    gem.authors = ["Jim Benton", "Maximilian Schulz", "Urban Hafner"]
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/*_test.rb'
  test.verbose = true
end

begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new do |test|
    test.libs << 'test'
    test.pattern = 'test/**/*_test.rb'
    test.verbose = true
  end
rescue LoadError
  task :rcov do
    abort "RCov is not available. In order to run rcov, you must: sudo gem install spicycode-rcov"
  end
end

task :test => :check_dependencies

task :default => :test

desc 'Generate RDoc documentation for the carmen plugin.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_files.include('README.rdoc', 'MIT-LICENSE').
    include('lib/**/*.rb')

  rdoc.main = "README.rdoc" # page to start on
  rdoc.title = "carmen documentation"

  rdoc.rdoc_dir = 'doc' # rdoc output folder
  rdoc.options << '--webcvs=http://github.com/jim/carmen/tree/master/'
end

namespace :import do
  desc 'Import country names from ZendFramework'
  task :zend do
    $KCODE="u"
    # The files can be found in library/Zend/Locale/Data in the ZendFramework
    input = File.expand_path(ENV['FILE'])
    require File.expand_path(File.join(File.dirname(__FILE__), 'lib', 'carmen'))
    require 'nokogiri'
    require 'yaml'
    doc = Nokogiri::XML(File.open(input))
    translated = Carmen.countries.map do |name, code|
      [doc.css("territory[type=#{code}]").first.content, code]
    end
    l = File.basename(input, ".*")
    File.open(File.join(File.dirname(__FILE__), "countries.#{l}.yml"), 'w') do |f|
      YAML.dump(translated, f)
    end
  end
end