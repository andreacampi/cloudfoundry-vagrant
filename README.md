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

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
