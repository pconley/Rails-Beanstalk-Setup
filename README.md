# Rails Beanstalk Setup


> rails new bean3
> cd bean3
> git init
> git add .
> git commit -am “generated app”
> rails s    # this will run on the mac
// note puma is already in the Gemfile
> eb init
	>> VA; New App; bean3; 
	>> Y (ruby); 2.4; N (code commit)
	>> N (SSH)
// note this changed the .gitignore, so
> git status
> git add .
> git commit -am “after eb init”
> eb create bean3-env
// WAIT… can go to console to see what is happening
// ERROR… it will give err message; but keep going
!!!! move the “gem listen” out of the development group to
!!!! the top level in the gem file… the NOT shown in the doc
> git status
> git add .
> git commit -am “moved the listen gem”
// set the env to dev on the eb instance
eb setenv RACK_ENV=development
// set the random string for security
eb setenv SECRET_KEY_BASE=1234somerandomkey5678
eb deploy     # for gemfile change
eb open
### make classic Widget changes ###
!! git add and commit
!! migrate db (locally)
!! rails s # to test locally
> eb printenv
# note skip migration is set to false so should auto migrate
> eb setenv RACK_ENV=production
> eb deploy
> eb open
