task :default do
  sh "rm -fr _site"
  sh "bundle exec jekyll build"
  sh "rm -fr _site/awscli-bundle.zip"
  sh "rm -fr _site/awscli-bundle"
  sh "rm -fr _site/ssl-challenge" # Remove that folder before we sync with the other site
  sh "aws s3 sync ./_site s3://theunicornfactory.is --region us-east-1 --exclude '.DS_Store' --exclude 'LICENCE' --exclude 'CNAME' --exclude 'node_modules/*' --exclude '.git/*' --exclude '.gitignore' --exclude 'Gemfile*' --exclude 'Rakefile' --exclude 'awscli-bundle*' --exclude 'ssl-challenge/*' --exclude '*.md' --acl public-read"
end

task :preflight do
    puts "Install bundler"
    sh "bundle install"
end

task :clean do
    puts "Cleanup all stuff"
    sh "rm -fr _site"
end

task :serve do
  sh "rm -fr _site"
  sh "bundle exec jekyll serve"
end

task :servedrafts do
  sh "rm -fr _site"
  sh "bundle exec jekyll serve --drafts"
end

# Just a simple rake task which helps sync whats in the SSL challenge directory (not runnable from CI)
task :sslchallenge do
  sh "aws s3 sync ./ssl-challenge s3://theunicornfactory.is/.well-known/acme-challenge --region us-east-1 --acl public-read"
end
