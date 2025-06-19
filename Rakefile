#!/usr/bin/env ruby

desc "Install and build"
task default: [:install, :build]

desc "Install gems"
task :install do
  sh "bundle config set --local path vendor/bundle"
  sh "bundle install"
end

desc "Build the blog using Jekyll"
task :build do
  sh "JEKYLL_ENV=production bundle exec jekyll build --trace"
end

desc "Run a local web server using Jekyll"
task :server => :build do
  sh "bundle exec jekyll server --trace --livereload"
end

desc "Upload the files in _site to the public webserver"
task :upload => :build do
  sh "rsync -avz _site/ www.aelius.com:~/www/www.aelius.com/njh/"
end
task :publish => :upload

desc "Deleted all the generated files (based on .gitignore)"
task :clean do
  File.foreach('.gitignore') do |line|
    # For safety
    next unless line =~ /^[\.\w]+/
    sh 'rm', '-Rf', line.strip
  end
end

