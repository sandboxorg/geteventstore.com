---
title: "v2.0 binaries released"
date: 2013-07-19T17:40Z
author: "Greg Young"
layout: blog-post
---

Version 2.0 binaries are now available for download at <a href="http://download.geteventstore.com/">http://download.geteventstore.com/</a>.

The new version is fully compatible with all database files from old versions no data upgrade is required. With the addition of security you will likely get asked for a username/password, the default is admin:changeit

## Major Changes

- Authentication over HTTP using basic authentication
- Authentication over TCP for built-in user accounts
- Management of internal accounts and ACLs
- Changed configuration now supports environmnet variables and config files
- Tcp client can now run over SSL
- `$stream-created` events removed from streams
- Stream metadata separated
- Better AtomPub compliance
- SSL + authentication for web console
- Trusted intermediaries
- Separated internal/external networks (ha only)
- SSL for replication channels (ha only)
- SSL for manager connections (ha only)
- Ability to disable routing (ha only)

## Summary

The largest single change in moving to 2.0 is the addition of <a href="https://github.com/EventStore/EventStore/wiki/HTTP-Security">security</a>. Security allows for both locking down the Event Store and setting up <a href="https://github.com/EventStore/EventStore/wiki/HTTP-Security">Access Control Lists </a>on streams. This can allow to control not just access to the stream but how people are allowed to access the stream.

In adding security to the system it also became necessary to support SSL on the various forms of connecting to the Event Store. As such the Client API (.net) and the <a href="https://github.com/EventStore/EventStore/wiki/Setting-Up-SSL-In-Windows">Atom interface</a> in the Single Node version now both support SSL. In the HA clustered version SSL has been added to the replication channels and all other internal communications as well. The HA version has also had all internal vs external traffic segmented so it can be run with internal traffic on a different network than client traffic.

The AtomPub interface has also had quite a few small changes to better represent the atom protocol. There is no longer a special type that gets posted to the resource instead all of the information from that type is put into http headers such as <a href="https://github.com/EventStore/EventStore/wiki/HTTP-Expected-Version-Header">ES_ExpectedVersion</a>. The differences can be seen in how you <a href="https://github.com/EventStore/EventStore/wiki/Writing-to-a-Stream-(HTTP)">write to a stream</a>.

Projections can now be considered in a beta stage. We have a few more changes we want to get in before calling it officially released and we have a ton of documentation to write on it but the chances of the language changing are low.

The configuration system has also had a major overhaul. Command line options are great but when you start getting <a href="https://github.com/EventStore/EventStore/wiki/Command-Line-Arguments">many of them</a> it also nice to be able to use environment variables or config files. All options can now be set through any of the three mechanisms. This is particularly useful when dealing with the HA version as you can centralize management easily.

Version 2.0 will install and use the same database as all previous versions. When using 2.0 however you must upgrade your .NET client api to 2.0 as well its <a href="https://nuget.org/packages/EventStore.Client/">on nuget</a>. This is largely due to the security changes. We do not foresee having any further client/server mismatches in the medium term (12 months) though its likely longer. Another change you will notice is that the $stream-created events no longer get created in your stream (when you create a stream there will be 0 events in it).

You may also notice we have quite a few more <a href="https://github.com/EventStore/EventStore/wiki/_pages">docs</a> there will be many more coming!

## The Future

We will also be changing a bit our release cycles. We expect to be seeing many minor releases to master and binaries dropped for them, likely around once per week. Periodically we will be releasing new "stable" drops that have gone through a full period of stress testing (beyond the continuous automated stress testing). As such more people will be able to test bleeding edge if they want in development or staging environments.

There will be many new features coming out the next few months including memory only usage, projections, and quite a few surprises!