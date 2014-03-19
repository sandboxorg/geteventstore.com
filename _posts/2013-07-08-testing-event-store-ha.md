---
title: "Testing Event Store HA"
date: 2013-07-08T18:21Z
author: "Greg Young"
layout: blog-post
---

As we prepare to release Event Store 2.0.0 binaries (the source code was just merged to the master branch over on <a href="http://github.com/EventStore/EventStore" title="GitHub" target="_blank">GitHub</a>), we also will be opening up access to one of the test environments that we've been using for our commercial high availability clustered product, Event Store HA.

We get many questions asking how the clustered version behaves during network partitions and server failures - <a href="http://ha.geteventstore.com">now you can see for yourself</a>!

<figure>
	<img src="{{ site.url }}/images/blog-ha-setup.jpg" alt="One of our test clusters">
</figure>

The cluster in the picture above is now <a href="http://ha.geteventstore.com/">connected to the web</a> to allow people to see a cluster in action, as well as some of the testing we perform on them. This particular cluster is running a power outage test (and has been for some time). We can also test network partitions both of which the cluster can easily handle.

We pull the power on a node programmatically using the device seen here:

<figure>
	<img src="{{ site.url }}/images/blog-power-switch.jpg">
</figure>

Cutting the power as opposed to just killing the process is a very important test for any database, as it tests the true durability of the data (including all the <a href="https://github.com/EventStore/EventStore/wiki/Reliability" title="Event Store - Reliability" target="_blank">liars like Intel 520 SSDs, or sneaky operating system caching!</a>). It also helps ensure our cluster election logic works reliably and quickly.

The test brings up a running cluster, then pulls the power on a random node in that cluster. Within about 60 seconds the node will start rebooting as power returns (the nodes themselves wait for power to be sustained to prevent damage due to cycling power). The node will then start up and verify its data before rejoining the cluster. After about one second of a node rejoining the test will rinse and repeat.

As of now, this particular cluster (Event Store HA 2.0.0 running on Windows and .NET) does roughly 1000 power pulls per day.

Would we be comfortable pulling power in production? Absolutely!