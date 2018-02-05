# Role of identifiers, addressing and service discovery in IoT


## Basic Terminologies 

**Naming convention :** is a set of rules defined for constituting an
identifier. For e.g., domain names should be constituted following the naming
convention as explained in [RFC1035](https://tools.ietf.org/html/rfc1035) 

**Identity :** is something which is definable and recognisable. It need not be
unique in a specific scope. A classic identity example is a person's name. A
name does not need to follow a specific *naming convention*. There are example
of names not only with alphabets (e.g. John Paul-II) 

**Identifier :** could be a physical (e.g. passport number) or virtual (e.g.
ToDo) identifier. It is used to identify an entity individually. It need to be
*unique* within a scope and should follow a specific *naming convention*. The
identifier will be the unique handle for the entity and will not change.

**Address :** is an identifier for the entity with an objective to communicate
with the entity such as MACID, IP addresses etc. It need to be *unique* within a
specific scope and should follow a specific *naming convention*.

**Service discovery :** a mechanism to relate an unique identifier to its
corresponding information. In the IoT paradigm, the service discovery could be
discovering an object associated with another identifier, its associated
metadata or a related service.


## Introduction 

There are sevaral definitions for IoT. In a nutshell, "IoT" is the Internet. In
the Internet, we have communication entities (devices) interconnected, such as
computer, mobile phones, routers etc. The IoT tries to go a step further and
interconnect all sorts of entities (things), such as human, cattle, bricks etc.
In order for these things to get interconnected, they need the support of
carrier devices. Examples of such carrier devices are RF-ID, Sensors, NFC etc.
This is the case in the Internet. For a computer to communicate, it needs a
carrier device such as network card; similarly, the mobile phones need a carrier
device such as SIM card.

The approach should be integrating the IoT entities to the Internet, which has
been operational for last thirty years. This is the reason, why all entities
whom have been part of the Internet eco-system, will also be part of the IoT
ecosystem. 

In the Internet, domain names, URI, IP addresses and DNS forms the corner stone
for identification/addressing and discovering associated data/devices related to
the identifier. 

## Problem statements

Currently we have plethora of IoT technologies. Each using its own set of
identifiers, naming conventions, namespaces and process of discovering. The
problem that arises due to this is that a "thing" using one technology (e.g.
Zigbee protocol) will not be able to communicate with a "thing" using another
technology (e.g. WiFi). In simple terms, the problem is *"interoperability"*. 

An ideal solution would be that all of them move to a single technology, which is
also not possible. The reason, being each of the IoT technologies satisfies a
niche market. The task of interoperating with different technologies is possibly
taken care by gateways, which acts as a bridge.

The issue then arises is that, how to uniquely identify a thing. Provisioning of
identifiers in the IoT field is not well regulated as in the Internet. In the
Internet, domain names and IP addresses have their own namespaces and managed in
a hierarchical distributed manner.    
  
