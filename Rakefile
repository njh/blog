#!/usr/bin/env ruby

desc "Build the blog using Jekyll"
task :build do
  sh "bundle exec jekyll build"
end

desc "Run a local web server using Jekyll"
task :server => :build do
  sh "bundle exec jekyll server"
end

desc "Upload the files in _site to the public webserver"
task :upload => :build do
  sh "rsync -a _site/ njh@www.aelius.com:~/public_html/"
end

desc "Deleted all the generated files (based on .gitignore)"
task :clean do
  File.foreach('.gitignore') do |line|
    # For safety
    next unless line =~ /^[\.\w]+/
    sh 'rm', '-Rf', line.strip
  end
end


task :default => :build
task :publish => :upload
