---
title: "Version 2.0.1 released"
layout: blog-post
author: "Greg Young"
date: 2013-08-01T17:15Z
---

As we have said before we will be moving to much faster release cycles. Along with this we will periodically be releasing long term supported stable releases that go through far more stress testing than our weekly to biweekly releases. We will be keeping semantic versioning for all releases.

For this release you probably want to upgrade. We admit it—we were muppets. One of the changes in the release is to lock down the admin operations in the Open Source version such as force scavenging. This does not affect anyone using the commercial version as in the commercial version all admin operations are run on a separate interface than the public interface.

Along with this there are some other changes in regard to ACLs. We have allowed the creation of custom default ACLs and allowed inheriting. This also allows for the assigning of permissions to create a stream. You can read more about how this works in the <a href="https://github.com/EventStore/EventStore/wiki/Access-Control-Lists">documentation</a>.

There was also a small problem with the chat sample. It was sending the wrong accept header (`vnd.eventstore.atom+json` instead of `application/vnd.eventstore.atom+json`). The chat sample and related browser hosted projection code is now working.

We have also added some code to bomb out if run in mono versions that we really don't think you should be running in (like 2.6 with boehm gc!). These can be overridden using the `--force` command line parameter if you really want to run in such environments.