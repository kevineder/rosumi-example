rosumi-example
==============

This project demonstrates the usage of the [Rosumi gem](https://github.com/kevineder/rosumi).

###Get device ids.
`bundle exec rake get_device_ids`
###Locate device 1
`bundle exec rake "locate_device[1]"`
###Send a message to device 1
`bundle exec rake 'message_device[1,"A Subject", "Hello world!",false]'`
