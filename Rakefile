#!/usr/bin/env rake
require 'bundler'
Bundler::GemHelper.install_tasks

desc 'Configure then bundle the gem'
task :bundle do

  ## begin bootstrap config ##

  sh 'rm -f app/assets/fonts/twitter/bootstrap/*.*'
  sh 'cp -f bootstrap/fonts/*.* app/assets/fonts/twitter/bootstrap'

  sh 'rm -f app/assets/javascripts/twitter/bootstrap/*.js'
  sh 'cp -f bootstrap/js/*.js app/assets/javascripts/twitter/bootstrap'

  sh 'rm -f vendor/toolkit/twitter/bootstrap/*.less'
  sh 'cp -f bootstrap/less/*.less vendor/toolkit/twitter/bootstrap'

  sh 'thor setup:bootstrap_update_less_files_for_asset_pipeline'
  sh 'thor setup:bootstrap_update_js_files_compilation_order'

  sh 'cp -f vendor/toolkit/twitter/bootstrap/bootstrap.less lib/generators/bootswatch/install/templates/bootstrap.less'

  sh 'cp -f vendor/toolkit/twitter/bootstrap/variables.less lib/generators/bootswatch/install/templates/variables.less.tt'
  sh 'cp -f vendor/toolkit/twitter/bootstrap/mixins.less lib/generators/bootswatch/install/templates/mixins.less.tt'

  sh 'thor setup:bootstrap_update_less_files_with_theme_info'

  sh 'thor setup:remove_imports_from_theme_less'

  ## end bootstrap config ##

  sh 'gem build twitter-bootswatch-rails.gemspec'

  require 'twitter/bootswatch/rails/version'

  sh "gem install twitter-bootswatch-rails-#{Twitter::Bootswatch::Rails::VERSION}.gem --local"

end

task(:default).clear
task :default => :bundle

desc 'Clean up files'
task :clean do

  sh "rm twitter-bootswatch-rails-#{Twitter::Bootswatch::Rails::VERSION}.gem"

end