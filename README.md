cas-clients-simple
==================

This project contains two clients who share a user database but would have different hostnames.  

Through the use of the [devise_cas_authenticatable gem](https://github.com/nbudin/devise_cas_authenticatable) they are able to have a single sign-on by logging on through a Central Authentication Service (via the [CASino ruby implementation](http://casino.rbcas.com) of the [CAS protocal](http://www.jasig.org/cas)).  The CAS-server points to the same user database as the client apps but maintains it's own database for tracking the sessions.  

Each client app defers the login process to the CAS server which redirects back to the originating server after authentication is successful.  The login form can be styled to match the client apps or the RESTful api can be used to create a ProxyTicket authentication.

Each client is a simple Ruby on Rails (4) app, using [Devise](https://github.com/plataformatec/devise) for authentication - Devise is deferring to CAS-server for authentication (configured in the /config/initializers/devise.rb)

SSL is recommended even for local [here is a great gist for setting up local self-signed certs](https://gist.github.com/trcarden/3295935)  

usage
=====
- install, configure and launch the CASino (or other CAS server) (launch using port 3000)
- clone this repo, `cd` into client-app-1, run a `bundle install`, configure the database.yml to match your database setup, `rake db:migrate` - client1 should be ready to launch (launch using port 3001)
- `cd` into client-app-2, run a `bundle install`, configure database.yml, use the same database as client1 since the only table is the user database. - client2 should be ready to launch (launch using port 3002)
- edit /etc/hosts to create different hostnames for each client to ensure the sessions are indeed spanning distinct hostnames
- load the root of the either client site and notice the 'casino' login screen, login - you should be redirected back to the client you initially requested.
- load the root of the other client, you should already be logged in.
- inspect the session cookie in either client session and see there are 2 distinct sessions
- single sign-out isn't working in this demo yet.
