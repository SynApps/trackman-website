# This file is used by Rack-based servers to start the application.
require ::File.expand_path('../config/environment',  __FILE__)
require 'toto'

# Rack config
use Rack::Static, :urls => ['/css', '/js', '/images', '/favicon.ico'], :root => 'blog/public'
use Rack::CommonLogger

if ENV['RACK_ENV'] == 'development'
  use Rack::ShowExceptions
end

Toto::Paths[:templates] = "blog/templates"
Toto::Paths[:pages] = "blog/templates/pages"
Toto::Paths[:articles] = "blog/articles"

toto = Toto::Server.new do
  set :prefix,      "blog"
  # set :author,    ENV['USER']                               # blog author
  # set :title,     'TRACKMAN'                  	      # site title
  # set :root,      "index"                                   # page to load on /
  # set :date,      lambda {|now| now.strftime("%d/%m/%Y") }  # date format for articles
  # set :markdown,  :smart                                    # use markdown + smart-mode
  set :disqus,      'blog-trackman'                           # disqus id, or false
  # set :summary,   :max => 150, :delim => /~/                # length of article summary and delimiter
  # set :ext,       'txt'                                     # file extension for articles
  # set :cache,      28800                                    # cache duration, in seconds
  set :date, lambda {|now| now.strftime("%B #{now.day.ordinal} %Y") }

end

map '/blog' do
	run toto
end

map '/' do
	run TrackmanWebsite::Application
end
