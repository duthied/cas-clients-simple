cas-clients-simple
==================

This project contains two clients who share a user database but would have different hostnames.  

Through the use of the [devise_cas_authenticatable gem](https://github.com/nbudin/devise_cas_authenticatable) they are able to have a single sign-on by logging on through a Central Authentication Service (via the [CASino ruby implementation](http://casino.rbcas.com) of the [CAS protocal](http://www.jasig.org/cas))  

Each client app defers the login process to the CAS server which redirects back to the originating server after authentication is successful.  The login form can be styled to match the client apps or the RESTful api can be used to create a ProxyTicket authentication.

Each client is a simple Ruby on Rails (4) app, using [Devise](https://github.com/plataformatec/devise) for authentication - Devise is deferring to CAS-server for authentication (configured in the /config/initializers/devise.rb)

SSL is recommended even for local [here is a great gist for setting up local self-signed certs](https://gist.github.com/trcarden/3295935)  
