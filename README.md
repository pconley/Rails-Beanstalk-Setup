# Rails Beanstalk Setup
These are my note from using the AWS walkthru document at XXX which is very good and has realy one one error (at the time of this writing).  For some reason the listen gem needs to be at the top level of the gemfile and not in the development section.
## Create a normal rails base app
```
rails new bean3
cd bean3
git init
git add .
git commit -am “generated app”
rails s    # test taht this will run on the mac
rails g scaffold Widget name:string owner:string size:integer
vi Gemfile        # move the listen gem to top level
vi config/routes  # to add a root as... root 'widgets#index'
git status
git add .
git commit -am “basic changes”
```
Note puma is already in the generate Gemfile so we do not have to add it as outlined in the doc.
## Elastic Beanstak Setup
```
eb init
	>> VA; 
	>> New App; 
	>> bean3; 
	>> Y (ruby); 
	>> 2.4; 
	>> N (code commit)
	>> N (SSH)
```
Note this changed the .gitignore, so
```
git status
git add .
git commit -am “after eb init”
```
Create the environment.  Note: we are by-passing the whole development branch of the walkthrough and
setting up everything fro production from the start.  Including setting environment variables that 
we do not want to set in the source code.
```
eb create bean3-env
eb setenv SECRET_KEY_BASE=1234somerandomkey5678
eb open
```
## After any updates

### make classic Widget changes ###
```
git add .
git commit -am "my changes"
rake db:migrate 
rails s    # to test locally
```
Note that skip migration is set to false so should auto migrate
```
eb printenv
```
eb deploy
eb open
