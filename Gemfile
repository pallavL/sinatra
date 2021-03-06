# Why use bundler?
# Well, not all development dependencies install on all rubies. Moreover, `gem
# install sinatra --development` doesn't work, as it will also try to install
# development dependencies of our dependencies, and those are not conflict free.
# So, here we are, `bundle install`.
#
# If you have issues with a gem: `bundle install --without-coffee-script`.

RUBY_ENGINE = 'ruby' unless defined? RUBY_ENGINE
source :rubygems unless ENV['QUICK']

gem 'rake'
gem 'rack-test', '>= 0.5.6'

# Allows stuff like `tilt=1.2.2 bundle install` or `tilt=master ...`.
# Used by the CI.
github = "git://github.com/%s.git"
repos = { 'tilt' => github % "rtomayko/tilt", 'rack' => github % "rack/rack" }
%w[tilt rack].each do |lib|
  dep = (ENV[lib] || 'stable').sub "#{lib}-", ''
  dep = nil if dep == 'stable'
  dep = {:git => repos[lib], :branch => dep} unless dep =~ /(\d+\.)+\d+/
  gem lib, dep
end

gem 'haml', '>= 3.0', :group => 'haml'
gem 'sass', :group => 'sass'
gem 'builder', :group => 'builder'
gem 'erubis', :group => 'erubis'
gem 'less', :group => 'less'
gem 'liquid', :group => 'liquid'
gem 'nokogiri', :group => 'nokogiri'
gem 'slim', :group => 'slim'
gem 'RedCloth', :group => 'redcloth' if RUBY_VERSION < "1.9.3"
gem 'coffee-script', '>= 2.0', :group => 'coffee-script'
gem 'rdoc', :group => 'rdoc'
gem 'kramdown', :group => 'kramdown'
gem 'maruku', :group => 'maruku'
gem 'creole', :group => 'creole'

platforms :ruby do
  gem 'rdiscount', :group => 'rdiscount'
  ## bluecloth is broken
  #gem 'bluecloth', :group => 'bluecloth'
end

platforms :ruby_18, :jruby do
  gem 'json', :group => 'coffee-script'
  gem 'markaby', :group => 'markaby'
  gem 'radius', :group => 'radius'
end

platforms :mri_18 do
  # bundler platforms are broken
  next if RUBY_ENGINE != 'ruby' or RUBY_VERSION > "1.8"
  gem 'rcov', :group => 'rcov'
end
