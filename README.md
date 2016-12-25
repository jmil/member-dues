# member-dues
In Three Steps:

1. Deploy this code
2. Collect membership dues via credit card
3. Profit!!!



## Connected Parts

• Website source code is [Rails 5](http://rubyonrails.org "Rails 5 FTW")
• Credit card handling is done by [Stripe](http://Stripe.com)
• Webhosting is done by [Heroku](http://Heroku.com)
• Collaborate on this code via [Github](http://github.com)

##Requirements
This is a [Rails 5](http://rubyonrails.org "Rails 5 FTW") app. It was fast and easy enough to get started.


##Instructions

### Quick Start:

1. You can simply clone this app and work on it like any other rails app.
	
		$ git clone https://github.com/jmil/member-dues.git
		$ cd member-dues
		$ bundle install
		$ rake db:create
	
1. Test functionality with dummy Stripe keys:

		$ PUBLISHABLE_KEY=pk_test_rxoZuyJe2us6IaFWXVOSSLEp SECRET_KEY=sk_test_kOutrH0hrnBZKKl9ZSzDyZ5M rails s
		
	Navigate to http://localhost:3000/ and see if you can make a test CC charge. Use Dummy CC# `4242 4242 4242 4242`.

1. Profit!!!

###More Details

Here's what I did to get this up and running:

1. Create a [Stripe](http://Stripe.com) account. To activate and begin to receive $$ you will need to enter bank account info and validate your account with personal info.

1. Install [RVM](https://rvm.io/rvm/install "RVM") or some other ruby environmental manager. I used rails 5.0.1 with ruby 2.3.3 for the instructions below. So you will need at least these versions.

1. Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install). Not strictly necessary, but super useful via command-line.

1. Install [postgresql]() database. On a Mac I followed this tutorial:
	https://gorails.com/setup/osx/10.12-sierra

		$ brew install postgresql
	Then it says to setup `postgresql` by default on system boot, so do this:
		
		# To have launchd start postgresql at login:
		$ ln -sfv /usr/local/opt/postgresql/*plist ~/Library/LaunchAgents


1. Continue working in the terminal by following this tutorial:
https://devcenter.heroku.com/articles/getting-started-with-rails5

	Note, you will need to use `postgresql` as the database, because sqlite3 is NOT allowed by Heroku. I did something like this:

		$ rails new member-dues --database=postgresql
		$ cd member-dues
		$ git init
		$ git add .
		$ git commit -a -m "initial commit"
		$ bundle install
		$ rake db:create ## THIS IS CRITICAL to initiate the postgresql database
		
	Now test that the server works:
	
		$ rails s
	
	Navigate to: http://localhost:3000/
	If you didn't receive any errors, and you see the Rails welcome, you are golden.
	
	
1. According to the Heroku tutorial:
https://devcenter.heroku.com/articles/getting-started-with-rails5
>Rails 5 no longer has a static index page in production. When you’re using a new app, there will not be a root page in production, so we need to create one. We will first create a controller... for our home page to live

	But that's fine, we are going to make the member dues charge page anyway and make that the homepage.
	
	Follow this tutorial:
	https://stripe.com/docs/checkout/rails
	
	Edit the `Gemfile` and add:
		
		# Add Stripe gem so we can take payments via credit cards
		gem 'stripe'

		
	near the top.
	
	then back in the terminal:
	
		$ bundle install
	
	to install the gem.
	
	Then create the membership controller: 
		
		$ rails g controller memberships
	
	Make **SURE** you use **PLURAL** names for your controllers. Controller name `membership` as singular will **NOT** work properly.
	
	Follow the rest of the stripe tutorial. Eventually you will want to test locally with test stripe public and secret keys, you can use these test keys:
	
		$ PUBLISHABLE_KEY=pk_test_rxoZuyJe2us6IaFWXVOSSLEp SECRET_KEY=sk_test_kOutrH0hrnBZKKl9ZSzDyZ5M rails s

	Test charge with dummy CC# `4242 4242 4242 4242`, it should process successfully. Yay!

	
1. Although this is just the skeleton, let's immediately deploy it to [Heroku](http://www.heroku.com) to make sure all the pieces fit together. Choose a Heroku app name (I suggest 'members-YourOrganization'). You can change this later with your web hosting provider to point to the Heroku DNS. Let's just get it working.

		$ heroku login
		$ heroku apps:create members-YourOrganization
		$ git remote -v
		$ git push heroku master
		
	Setup Heroku with test keys:
	
		$ heroku config:set PUBLISHABLE_KEY=pk_test_rxoZuyJe2us6IaFWXVOSSLEp SECRET_KEY=sk_test_kOutrH0hrnBZKKl9ZSzDyZ5M

	Your site should now be live at http://members-YourOrganization.herokuapp.com and you should be able process a test charge.
	
	Refer to Heroku documentation for how to have your domain name (such as yourorganization.org) point to Heroku and make the user experience more optimal.


## References

Follow these tutorials:

Rails 5 application deployment to Heroku:
https://devcenter.heroku.com/articles/getting-started-with-rails5#deploy-your-application-to-heroku

Stripe Checkout via Rails:
https://stripe.com/docs/checkout/rails

