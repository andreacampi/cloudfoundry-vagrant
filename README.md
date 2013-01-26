# Cloud Foundry on Vagrant

Spin up a local [Cloud Foundry](http://www.cloudfoundry.org) installation
using Vagrant, in a variety of topologies.

Supported topologies:

* [single node](single-node/README.md);
* more coming soon.

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

When done, you have a running CloudFoundry / VCAP VM running; which can be accessed via the localhost:9080 NAT created by vagrant.

Follow [these instructions to try out your setup](https://github.com/cloudfoundry/oss-docs/tree/master/vcap/single_and_multi_node_deployments_with_dev_setup#trying-your-setup), remembering that your API url is: ```http://api.vcap.me:9080```

## Configuration

You can fine-tune your Cloud Foundry installation by setting a few attributes:

* `node['cloudfoundry_cloud_controller']['server']['services']` - an Array of
services that you want to support in your setup.

Some attributes control more advanced aspects of your cluster; you should
be careful when changing those, and make sure you understand the consequences:

* `node['cloudfoundry_cloud_controller']['server']['api_url']` - internal URL
for Cloud Foundry components that need to connect to the `cloud_controller`.
This may be different from the public URL, depending on your topology.
Defaults to `http://api.vcap.me:9200`.

The underlying cookbooks declare a lot more tunable attributes. Some of them
are relevant for a production setup, and they will be documented in this
document in the near future; others are internal or very advanced. You can
find a complete list of tunable attributes by perusing the documentation for
each cookbook:

* [general](https://github.com/zephirworks/cloudfoundry-cookbook.git);
* [cloud_controller](https://github.com/zephirworks/cloudfoundry-cloud_controller-cookbook.git);
* [health_manager](https://github.com/zephirworks/cloudfoundry-health_manager-cookbook.git);
* [router](https://github.com/zephirworks/cloudfoundry-router-cookbook.git)
and the underlying [nginx](https://github.com/zephirworks/cloudfoundry-nginx-cookbook.git);
* [stager](https://github.com/zephirworks/cloudfoundry-stager-cookbook.git);
* [DEA](https://github.com/zephirworks/cloudfoundry-dea-cookbook.git) and the
supported runtimes:
 * [ruby](https://github.com/zephirworks/cloudfoundry-ruby-runtime-cookbook.git);
* [services](https://github.com/zephirworks/cloudfoundry_service-cookbook.git):
 * [filesystem](https://github.com/zephirworks/cloudfoundry-filesystem-service-cookbook.git);
 * [mongodb](https://github.com/zephirworks/cloudfoundry-mongodb-service-cookbook.git);
 * [rabbitmq](https://github.com/zephirworks/cloudfoundry-rabbitmq-service-cookbook.git).

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
