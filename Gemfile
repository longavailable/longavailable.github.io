source "https://rubygems.org"

gem "jekyll", "~> 4.1.1"

# Replaced by the remote-theme:minima supported by 'jekyll-remote-theme'
#gem "minima", git: "https://github.com/jekyll/minima"

group :jekyll_plugins do
  gem 'jekyll-feed', "~> 0.12"
  gem 'jekyll-sitemap'
  gem 'jekyll-seo-tag'
  gem 'jekyll-remote-theme'
  #gem 'jekyll-admin'
  gem 'jekyll-paginate'
  gem 'jekyll-spaceship', git: 'https://github.com/jeffreytse/jekyll-spaceship' #, ref: '935ce5'
  #gem 'jekyll-pandoc'
  gem 'jekyll-redirect-from'
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

gem "webrick"
