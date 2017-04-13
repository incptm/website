# encoding: utf-8

require 'rubygems'
require 'rake'
require 'tempfile'
require 'rake/clean'
require 'scss_lint/rake_task'
require 'nokogiri'
require 'rubocop/rake_task'
require 'English'
require 'net/http'
require 'html-proofer'

task default: [
  :clean,
  :build,
  :pages,
  :garbage,
  :rubocop
]

def done(msg)
  puts msg + "\n\n"
end

desc 'Delete _site directory'
task :clean do
  rm_rf '_site'
  done 'Jekyll site directory deleted'
end

desc 'Build Jekyll site'
task :build do
  if File.exist? '_site'
    done 'Jekyll site already exists in _site'
  else
    system('jekyll build')
    fail 'Jekyll failed' unless $CHILD_STATUS.success?
    done 'Jekyll site generated without issues'
  end
end

desc 'Check the existence of all critical pages'
task pages: [:build] do
  File.open('_rake/pages.txt').map(&:strip).each do |p|
    file = "_site/#{p}"
    fail "Page #{file} is not found" unless File.exist? file
    puts "#{file}: OK"
  end
  done 'All files are in place'
end

desc 'Check the absence of garbage'
task garbage: [:build] do
  File.open('_rake/garbage.txt').map(&:strip).each do |p|
    file = "_site/#{p}"
    fail "Page #{file} is still there" if File.exist? file
    puts "#{file}: absent, OK"
  end
  done 'There is no garbage'
end

desc 'Run RuboCop on all Ruby files'
RuboCop::RakeTask.new do |t|
  t.fail_on_error = true
  t.requires << 'rubocop-rspec'
end
