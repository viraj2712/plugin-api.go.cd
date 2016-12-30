require 'middleman-gh-pages'
require 'rake/clean'
require_relative "lib/version"

CLOBBER.include('build')

task :default => [:build]

task :publish do
  sh("aws s3 sync 'build' s3://#{ENV['S3_BUCKET']} --dryrun --cache-control 'max-age=600' --acl public-read")
end

Rake::Task[:publish].prerequisites.unshift "clobber"