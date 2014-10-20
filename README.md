@todo:
- Setup Bifrost github repo
  - git@github.com:Tetha/bifrost.git
- reach out to other mentors


bifrost-proposal
=================

# Abstract
Bifrost is a scalable time series storage backend. Its main purpose is for use
with Graphite but can be leveraged by any application needing time series 
storage.

# Proposal
Bifrost will provide a fully distributed, fault tolerant storage backend for
the Graphite monitoring project. Bifrost takes the place of Carbon in a normal
Graphite distribution. This makes it easier to implement a highly scalable,
fault tolerant storage for a Graphite instance.

# Background
Graphite is one of the most widely used monitoring solutions. The compelling
point of Graphite is it's approach to the monitoring problem: Instead of just
providing a mostly static view into the system like Munin, Graphite provides a
metric database.

This metric database is fed via various Carbon interfaces. For example, the
easiest interface to add data to Graphite is the plaintext protocol, which
accepts lines in the form "$metric $value $optionalTimestamp" via simple tcp
sockets.

On the other site, Graphite offers a REST-Interface to retrieve rendered PNGs,
simple JSON with the data. The data can be processed with a rich assortment of
functions and selected using wildcards, making it easy to perform queries such
as "Sum the requests per second across this set of hosts".

This decouples data collection and data access and makes it possible to analyze
highly complex systems with ease.

Graphite has one painful point, though: Data Storage. It's possible to scale
Graphite horizontally, but it's not trivial and takes quite a bit of effort.
However, graphite offers an interface to swap out the carbon storage and this is
precisely where bifrost enters the stage.

# Rationale
Bifrost enables Graphite to seamlessly scale by detaching the storage and UI
layers from each other. Due to this separation Bifrost enables a entirely new
set of capabilities for any time series data management needs. Our long term
vision is to grow a unified scalable monitoring community.

The initial requirements for Bifrost included:

 - Full Support for the Plaintext TCP Interface. This is necessary to support
 	tools such as Diamond, StatsD and any other existing applications
 - Full Support for the Storage API of Graphite
 - High performance for both Value and Key retrieval
 - Automated aggregation of data
 - Stability
 - Ability to be installable via configuration managemetn (puppet, chef, etc.)

# Current Status
Bifrost is currently deploying with a Graphite frontend as the replacement
for Munin at Goodgame Studios in a productive environment.

# Meritocracy
By submitting this incubator proposal, we're expressing our intent to build a
diverse developer community around Bifrost that will conduct itself according
to The Apache Way. We believe that this project enables a wide array of
possibilities within the monitoring ecosystem and will be the base for many new
users, including those in the Graphite communty, to be exposed to the Apache
way.

# Community
Bifrost will spark the interest of anyone interested in scalable monitoring
solutions and we hope to extend and grow our contributor base from the existing
Graphite monitoring community.

# Core Developers
The initial set of core developers are the Profiling Team at Goodgame Studios.
During the drafting of this proposal it was discovered that another company,
Acquia, has been working on an identical project and been contributing back to
the Graphite community as well. Goodgame Studios has inviting this team to join
the project to increase team diversity and help strengthen the Bifrost
community from the very begining.

# Alignment
The Apache Software Foundation is a natural fit to host the Bifrost project,
given the goal of open sourcing the project and fostering a community to grow
and support the software. Additionally, Bifrost leverages Apache Cassandra for
storage and Apache Thrift as a transport.

# Known Risks

## Orphaned Products
There are two companies currently focused on building entire production
monitoring systems on top of the Bifrost project. Thus, there is very little
risk of this project being orphaned.

## Inexperience with Open Source
The initial Bifrost committers have varying levels of experience using and
contributing to Open Source projects, however by working with our mentors and
the Apache community we believe we will be able to quickly embrace The Apache
Way.

## Homogenous Developers
Bifrost starting committers are comprised from two companies, Goodgame Studios
and Acquia. Our objective is to foster a collaberative community for anyone
seeking a scalable monitoring solution.

## Reliance on salaried developers
It is expected that Bifrost development will occur on both salaried time and on
volunteer time, after hours. The majority of initial committers are paid by their
employers to contribute to this project. However, they are all passionate about
the project, and we are confident that the project will continue even if no
salaried developers contribute to the project.

## Relationship with Other Apache Products
Currently, we use Apache Cassandra, Thrift, Commons Collections, Commons Lang
and Log4j. Further use into cluster management and control projects will be
investigated.

## A Excessive Fascination with the Apache Brand
Bifrost has already attracted a stable base of developers from multiple
companies. The reasons for joining Apache are not to advertise the project, but
rather to demonstrate the commitment to open source by fostering a community
focused on highly scalable monitoring and pursuing further integration with
other Apache projects.

# Documentation
This proposal is available at http://wiki.apache.org/incubator/BifrostProposal.
Basic build instructions and setup exist at the Bifrost github repository,
along with the source code having thorough documentation. As part of incubation
process we intend to improve our overall user documentation.

# Initial Source
Bifrost has been in active development since early 2014, maintained by a
varying team of developers. Currently, there are 6 active developers, though not
all are working on Bifrost full time, given that the monitoring is but one of
their responsibilies.

 - https://github.com/tetha/bifroest

# Source and Intellectual Property Submission Plan
A snapshot of the Bifrost storage backend has been posted to GitHub for review.
All code currently hosted under the github Bifrost project will be contributed
to the Apache Software Foundation. During incubation, the codebase will be
available at:

 - https://git-wip-us.apache.org/repo/asf/incubator-bifrost.git

mirrored at:

 - https://github.com/apache/incubator-bifrost/

# External Dependencies
All Bifrost dependencies have Apache compatible licenses.

# Required Resources

## Cryptography
Not applicable.

## Mailing lists

 - private@bifrost.incubator.apache.org (moderated subscription)
 - dev@bifrost.incubator.apache.org
 - commits@bifrost.incubator.apache.org

## Git Repositories

 - https://git-wip-us.apache.org/repo/asf/incubator-bifrost.git

## Issue Tracking

 - Jira: Bifrost (BIFROST)

# Initial Commiters

 - Harald Krämer (hkraemer at goodgamestudios dot com)
 - Sören Glimm (sglimm at goodgamestudios dot com)
 - Tobias Ruhe (truhe at goodgamestudios dot com)
 - Ole Claussen (oclaussen at goodgamestudios dot com)
 - Bianca Noack (bnoack at goodgamestudios dot com)
 - Antje Winker (awinker at goodgamestudios dot com)
 - Andrew Kenney (akenney at acquia dot com)
 - Dan Norris (dnorris at apache dot org)
 - Jake Farrell (jfarrell at apache dot org)

# Sponsors
## Champion
 - Jake Farrell (jfarrell at apache dot org)

## Nominated Mentors
 - Jan Iversen (jani at apache dot org)

## Sponsoring Entity
 - Apache Incubator PMC
