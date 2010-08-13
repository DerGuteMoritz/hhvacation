require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "hhvacation"
    gem.summary = %Q{A drop-in replacement for gnuhh hhvacation}
    gem.description = %Q{This is a drop-in replacement for the apparently no longer maintained hhvacation program included in the GNU Hosting Helper (http://hostingsoftware.net/) suite. It only operates on so called "virtual" vacation responds (i.e. they are kept in a MySQL database).}
    gem.email = "moritz@twoticketsplease.de"
    gem.homepage = "http://github.com/DerGuteMoritz/hhvacation"
    gem.authors = ["Moritz Heidkamp"]
    gem.add_dependency 'mail'
    gem.add_dependency 'mysql'
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new do |test|
    test.libs << 'test'
    test.pattern = 'test/**/test_*.rb'
    test.verbose = true
  end
rescue LoadError
  task :rcov do
    abort "RCov is not available. In order to run rcov, you must: sudo gem install spicycode-rcov"
  end
end

task :test => :check_dependencies

task :default => :test

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "hhvacation #{version}"
  rdoc.rdoc_files.include('README*')
end
