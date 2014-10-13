bifroest-proposal
=================

# Abstract
Bifroest will be a storage backend for Graphite based on Apache Cassandra.

# Proposal
Bifroest will provide a fully distributed, fault tolerant storage
backend for the Graphite monitoring project. Bifroest takes the place
of Carbon in a normal Graphite distribution. This makes it easier
to implement a highly scalable, fault tolerant storage for a Graphite
instance.

# Background
Graphite is one of the most widely used monitoring solutions. The 
compelling point of Graphite is it's approach to the monitoring 
problem: Instead of just providing a mostly static view into the
system like Munin, Graphite provides a metric database.

This metric database is fed via various Carbon interfaces. For 
example, the easiest interface to add data to Graphite is the 
plaintext protocol, which accepts lines in the form 
"$metric $value $optionalTimestamp" via simple tcp sockets.

On the other site, Graphite offers a REST-Interface to retrieve
rendered PNGs, simple JSON with the data. The data can be 
processed with a rich assortment of functions and selected
using wildcards, making it easy to perform queries such as
"Sum the requests per second across this set of hosts".  

This decouples data collection and data access and makes it possible
to analyze highly complex systems with ease.

Graphite has one painful point, though: Data Storage. It's
possible to scale Graphite horizontally, but it's not trivial 
and takes quite a bit of effort. However, graphite offers an
interface to swap out the carbon storage and this is precisely
where bifroest enters the stage.

# Rationale
Bifroest will simplify deployment and scaling of graphite a lot.
With Bifroest, there is no need to modify graphite configurations
when adding new nodes to the cassandra cluster, because Graphite 
only knows Bifroest. The storage cluster is completely hidden 
to the frontend. 

Furthermore, I think the ASF is the right place for a project like
this, because the ASF has a reputation for having very strong
and reliable infrastructural components, such as the Apache
webserver, Apache Hadoop, Apache Cassandra and so on. I think
Bifroest will fit right into this lineup.

# Current Status
At Goodgamestudios, we are currently deploying the current
version of Bifroest with a Graphite frontend as the replacement
for Munin as our productive environment. The requirements for
this include:

 - Full Support for the Plaintext TCP Interface. This is necessary
   to support tools such as Diamond, StatsD and a whole lot
   of other options
 - Full Support for the Storage API of Graphite. This is necessary
   to be considered any kind of a replacement for Carbon
 - High performance for both Value and Key retrieval
 - Aggregation of data in the database in order to not explode
   from too much data.
 - Stability. Current uptime is 1w and counting.
 - Full control via Chef.

# Meritocracy (TODOish: Not sure what really to write here?)

I'm very convinced that a project like this should be driven by
it's users. If someone has a compelling need for a feature, it
must be considered.  If a feature is considered, it is highly
beneficial to be able to lean on a community of experienced users
who can judge the features from more angles than any single
individual can.

# Community (TODO: Not sure what to write here) 

Bifroest will build on the monitoring and graphite community,
as well as sysadmin communities. 


# Core Developers (TODO: Not sure what to write here)

The core developers are the Profiling Team at Goodgame Studios,
and Jake Farrels team. 

# Alignment (TODO: Not sure what to write here)
On application level, we are heavily building on top of Apache
cassandra. Internally, Apache Commons and Apache Log4j are
used.

# Known Risks

## Orphaned Products
We are building our entire production monitoring on top of this
project. Thus, there is very little risk of this project
being orphaned.

## Inexperience with Open Source
Most initial committers from Goodgame Studios have submitted
patches to various open source projects, for example
Graphite Web, Gentoo, Munin or the AT Launcher. None of us
are majorly involved in an open source project yet though.

## Homogenous Developers

(TODO: Jake - what's your plan here?)

The developers from Goodgame Studios are all Java Developers
with more or less operational experience on unix systems, all
located in Hamburg, Germany. 

## Reliance on salaried developers

Currently, all development of bifroest occurs during salaried
time at goodgame studios. I (Harald) would personally volunteer
additional time, though, so the project would not evaporate
if the salaried developers stop contributing.

## Relationship with Other Apache Products
Currently, we use Apache Cassandra, Commons Collections, 
Commons Lang and Log4j. Further use into cluster
control projects are to be investigated.

## A Excessive Fascination with the Apache Brand

As stated above, the apache foundation has a reputation to
contain a number of very, very solid infrastructural projects,
such as the Apache Webserver, Apache Log4j and similar projects.
This, and our close ties to Apache Cassandra are the 
primary reasons why I chose the ASF as the first attempt to
include Bifroest as an open source project.

I hope that the Apache brand will give Bifroest the community
it needs to become one of the next big monitoring names.

# Documentation

Given that all of this is currently closed source, I cannot
easily link to the documentation, as little of it as exists.

# Initial Source

The code base is a software project at goodgame studios, under
development since about the beginning of 2014, maintained 
by a varying team of developers. Currently, we are at 6 
developers, though not all of them are working on this 
project full time, given that the monitoring is but one of our
responsibilies.

# Source and Intellectual Property Submission Plan

( TODO: uh, this seems kinda simple? )

Mostly, I plan to drop a bunch of code, some RPM-Specs and
some chef-configurations into several git repositories.

# External Dependencies

( TODO: not sure if this is detailed enough )

Our only external dependencies are Java and Apache Products.
These don't have Version issues.

# Required Resources

## Mailing lists

 - private@bifroest.incubator.apache.org (with moderated subscriptions)
 - dev@bifroest.incubator.apache.org
 - commits@bifroest.incubator.apache.org

## Git Repositories

( TODO: We are still splitting an internal library to hand out less code here )

 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-commons.git
 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-bifroest.git
 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-streamrewriter.git
 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-aggregator.git
 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-retentions.git
 - https://git-wip-de.apache.org/repo/asf/incubator-bifroest-commons.git

## Issue Tracking

 - Jira  Bifroest (OPEN-BF)

# Initial Commiters

( TODO: NDAs)

 - Harald Krämer (hkraemer@goodgamestudios.com)
 - Sören Glimm (sglimm@goodgamestudios.com)
 - Tobias Ruhe (truhe@goodgamestudios.com)
 - Ole Claussen (oclaussen@goodgamestudios.com)
 - Bianca Noack (bnoack@goodgamestudios.com)
 - Antje Winker (awinker@goodgamestudios.com)

 - Jake Farrel (jfarrel@apache.org)

# Sponsors
## Champion
 - Jake Farrel
