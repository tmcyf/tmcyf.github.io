require "rubygems"
require 'rake'
require "tmpdir"
require "bundler/setup"
require "jekyll"

desc "Automatically generate site at :4000 for local dev"
task :dev do
  system "jekyll serve --watch"
end # task :dev

desc "Remove _site from directory before committing"
task :clean do
  system "rm -rf _site"
end # task :clean

GITHUB_REPONAME = "tmcyf/tmcyf.github.io"

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp
    Dir.chdir tmp
    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master --force"
  end
end