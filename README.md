# Cloud Foundry on Vagrant

Spin up a local Cloud Foundry installation using Vagrant

## Installation

Install [Librarian-Chef](https://github.com/applicationsonline/librarian)

    $ gem install librarian

Then pull all the dependant cookbooks (as specified in chef/Cheffile)

    $ cd $YOUR_BASE_FOLDER/chef
    $ librarian-chef install 

Create your data_bags

    $ cd $YOUR_BASE_FOLDER/chef
    $ mkdir data_bags

Start up your virtualbox via Vagrant

    $ cd $YOUR_BASE_FOLDER/single-node
    $ vagrant up

This will take quite a while, so go grab a coffee

When done, you have a running CloudFoundry / VCAP VM running; which can be accessed via the localhost:9022 tunnel created by vagrant.

Follow [these instructions to try out your setup](https://github.com/cloudfoundry/oss-docs/tree/master/vcap/single_and_multi_node_deployments_with_dev_setup#trying-your-setup), remembering that your API url is: ```http://api.vcap.me:9022```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
