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

* `vmc` 0.4.x versions report a spurious error message after pushing your app:
<pre>
    Creating hello... FAILED
    CFoundry::NotFound: 404: &lt;!DOCTYPE HTML PUBLIC &quot;-//IETF//DTD HTML 2.0//EN&quot;&gt;
    &lt;html&gt;&lt;head&gt;
    &lt;title&gt;404 Not Found&lt;/title&gt;
    &lt;/head&gt;&lt;body&gt;
    &lt;h1&gt;Not Found&lt;/h1&gt;
    &lt;p&gt;The requested URL /apps/hello was not found on this server.&lt;/p&gt;
    &lt;/body&gt;&lt;/html&gt;

    For more information, see ~/.vmc/crash
</pre> Despite this message, the app has been pushed, but not started yet.
<pre>
    $ vmc app hello
    $ vmc start hello
</pre>
