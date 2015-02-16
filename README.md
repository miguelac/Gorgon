Gorgon
=====================

[![Gem Version](https://badge.fury.io/rb/gorgon.png)](https://rubygems.org/gems/gorgon)
[![Code Climate](https://codeclimate.com/github/Fitzsimmons/Gorgon.png)](https://codeclimate.com/github/Fitzsimmons/Gorgon)

About
---------------------

Gorgon provides a method for distributing the workload of running ruby test suites. It relies on amqp for message passing, and rsync for the synchronization of source code.

Installing Gorgon
-----------------
This [tutorial](/tutorial.md) explains how to install gorgon in a sample app. 

Installing listener as a Daemon process (Ubuntu 9.10 or later)
----------------------------------------------------------------
1. run `gorgon install_listener` from the directory where gorgon.json is
1. run `gorgon ping` to check if the listener is running

Gotchas
----------------------------------------------------------------

* if you get `cannot load such file -- qrack/qrack (LoadError)`, just add `gem 'gorgon', '~> 0.8.3' , :group => :remote_test` to your Gemfile, and run tests using `bundle exec gorgon`
* If `gorgon install_listener` didn't work for you, you can try [these steps](/daemon_with_upstart_and_rvm.md)

Also note that the steps in the tutorial are **not** meant to work on every project, they will only give you initial settings. You will probably have to modify the following files:
* gorgon.json
* {test, spec}/gorgon_callbacks/gorgon_callbacks.rb
* gorgon_listener.json (located in your project root or in ~/.gorgon/)

If you modify ~/.gorgon/gorgon_listener.json, make sure you restart the listener.

Configuration
---------------------

### gorgon.json
This file contains project-specific settings for gorgon, such as:

* The connection information for AMQP
* The connection information for File Server
* Information about how clients can rsync the working directory (optional). See more info [here](/rsync_transport.md) 
* Files that can be excluded by rsync
* Callback file containing Ruby code to be used as callbacks
* A glob for generating the list of test files
* The file used for Originator's logs

See [gorgon.json example](/gorgon.json.sample) for an example file.

### gorgon_listener.json
This file contains the listener-specific settings, such as:

* The connection information for AMQP
* How many worker slots are provided by this listener
* The file used for logs

See [gorgon_listener.json example](/gorgon_listener.json.sample) for more details.

Contributing
---------------------
Read overview [architecture](/architecture.md)

Credits
---------------------
Gorgon is maintained by:
* Justin Fitzsimmons
* Arturo Pie

Gorgon is funded by [Nulogy Corp](http://www.nulogy.com/).
Thank you to all the [contributors](https://github.com/Fitzsimmons/Gorgon/contributors).
