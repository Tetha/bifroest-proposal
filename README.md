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

# Meritocracy (TODOish)

I'm very convinced that a project like this should be driven by
it's users. If someone has a compelling need for a feature, it
must be considered.  If a feature is considered, it is highly
beneficial to be able to lean on a community of experienced users
who can judge the features from more angles than any single
individual can.

# Community (TODO) 

Bifroest will build on the monitoring and graphite community,
as well as sysadmin communities. 


# Core Developers (TODO)

The core developers are the Profiling Team at Goodgame Studios,
and Jake Farrels team. 


