require "rubygems"
require "bundler/setup"
require "fileutils"

ENV['LC_CTYPE'] = 'ru_RU.UTF-8'
ENV['LANG'] = 'ru_RU.UTF-8'

s3_bucket = "romanspiridonov.com"

desc "Deploy website via s3cmd"
task :deploy do
  puts "## Removing bad files"
  Dir['build/**/.DS_Store'].each{ |f| FileUtils.rm(f) }
  
  puts "## Deploying website via s3cmd"
  system("s3cmd sync --acl-public --reduced-redundancy build/* s3://#{s3_bucket}/")
  
  puts '## Done'
end

desc "Build website"
task :build do
  system("middleman build")
  
  Dir['build/**/b/'].each{ |f| FileUtils.rm_r(f) }
  (Dir['build/javascripts/*'] - ['build/javascripts/all.js']).each{ |f| FileUtils.rm_r(f) }
  (Dir['build/stylesheets/*'] - ['build/stylesheets/all.css']).each{ |f| FileUtils.rm_r(f) }
end

desc "Start dev server"
task :server do
  system("middleman server")
end