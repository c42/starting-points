require 'rspec/core/rake_task'
require 'metric_fu'

desc 'Create tasks to run unit tests'

RSpec::Core::RakeTask.new(:unit) do |t|
  t.pattern = './spec/unit/{,/*/**}/*_spec.rb'
end


desc 'Create tasks to run integration tests'

RSpec::Core::RakeTask.new(:integration) do |t|
  t.pattern = './spec/integration/{,/*/**}/*_spec.rb'
end


desc 'Default: run specs and generate metrics'

namespace :coverage do
  desc ""
  task :integration do
    ENV["COVERAGE"] = "disable"
    Rake::Task['integration'].invoke
  end

  desc ""
  task :unit do
    ENV["COVERAGE"] = "enable"
    Rake::Task['unit'].invoke
  end
end

task :default => ["coverage:unit", "coverage:integration", "metrics:all"]
