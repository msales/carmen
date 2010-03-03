require 'rubygems'
require 'rake'
require 'hanna/rdoctask'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "namxam-carmen"
    gem.summary = %Q{A collection of geographis country and state names for Ruby}
    gem.description = %q{A fork of the carmen gem by Jim Benton. This fork allows you to 
      switch between different locales (Currently english and german).
      A collection of geographis country and state names for Ruby. 
      Also includes replacements for Rails' country_select and state_select plugins.}
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
