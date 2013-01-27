# Setting up a small clustered installation

Note: this is preliminary documentation, to be turned into a real multi-VM
Vagrant setup.

This document assumes Chef solo.

## Goal

Set up a cluster of 4 nodes with:

* `node0` will run:
 * `nats-server`;
 * `cloud_controller`;
 * `health_manager`;
 * `stager`;
 * `router`;
 * service gateways for all the services.

* `node1` and `node2` will be set up as DEAs;

* `node3` is going to run service nodes.

## Run list

### `node0`

Note: we assume you have a PostgreSQL server available.

* `cloudfoundry_nats_server`;
* `cloudfoundry_redis_vcap`;
* `cloudfoundry_cloud_controller`;
* `cloudfoundry_health_manager`;
* `cloudfoundry_ruby_runtimes`;
* `cloudfoundry_stager`;
* `cloudfoundry_mongodb_gateway`;
* `cloudfoundry_rabbitmq_gateway`;
* `cloudfoundry_filesystem_gateway`.

### `node1` and `node2`

* `cloudfoundry_dea`;
* `cloudfoundry_ruby_runtimes`.

### `node3`

* `cloudfoundry_mongodb_node`;
* `cloudfoundry_rabbitmq_node`.

## Attributes

### Chef Solo

#### Required and recommended

On all nodes:

* `node['cloudfoundry']['domain']` should be set to the domain name under which
  your cluster will be accessible; this will be used to set default values for
  other variables;
* `node['cloudfoundry']['api_url']` should be set to the URL that you wish your
  `cloud_controller` to respond to; defaults to
  `"http://api.#{node['cloudfoundry']['domain']}"`;
* `node['cloudfoundry']['nats_server']['host']` must be explicitly set (on
  `node1..3`) to point to `node0`;
* `node['cloudfoundry']['nats_server']['user']` and
  `node['cloudfoundry']['nats_server']['password']` should be changed from the
  default; they should match `node['nats_server']['user']` and
  `node['nats_server']['password']` set on the Nats server;
* FIXME document vcap_redis

On `node0`:

* `node['cloudfoundry_cloud_controller']['database']` attributes (`host`,
  `port`, `user` and `password`, `name`) must be set as needed to connect to
  the cloud controller database;
* `node['cloudfoundry']['runtimes']`
