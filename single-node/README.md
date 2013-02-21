# Single-node installation

This Vagrant configuration sets up a single VM suitable for exploring
Cloud Foundry on your laptop.

Getting started is easy:

    $ vagrant up

The Cloud Foundry router will be configured to listen on port 9080:

    $ vmc target api.vcap.me:9080
    $ vmc push helloworld
    [follow the prompts and pick `helloworld.vcap.me:9080' as the app URL]
    $ curl http://helloworld.vcap.me:9080/

# Known issues

* `vmc` 0.3.x versions do not recognize the ruby19 runtime as default. As a
workaround, you can explicitly specify the runtime when first pushing your
app:
<pre>
    $ vmc push --runtime ruby19
</pre>
