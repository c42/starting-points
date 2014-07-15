require 'rspec/core/rake_task'
require 'metric_fu'
require 'simplecov'


MetricFu.configuration.configure_metrics.each do |metric|
  if [:churn, :flay, :flog].include?(metric.name)
    metric.enabled = true
  else
    metric.enabled = false
  end
end


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
  task :unit do
    SimpleCov.start do
      SimpleCov.coverage_dir 'coverage/unit/'
      Rake::Task['unit'].invoke
    end
  end
  desc ""
  task :integration do
    SimpleCov.start do
      SimpleCov.coverage_dir 'coverage/integration/'
      Rake::Task['integration'].invoke
    end

  end
end

task :default => ["coverage:unit", "coverage:integration", "metrics:all"]
