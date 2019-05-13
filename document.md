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

**Address :** is an identifier for the entity with an objective to communicate,
such as MACID, IP addresses etc. It needs to be *unique* within a specific scope
and should follow a specific *naming convention*.

**Service discovery :** a mechanism to relate an unique identifier to its
corresponding information. In the IoT paradigm, the service discovery could be
discovering an object associated with another identifier, its associated
metadata or a related service.


## Introduction 

There are several definitions for IoT. In a nutshell, "IoT" is the Internet. In
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
whom have been part of the Internet ecosystem, will also be part of the IoT
ecosystem. 

In the Internet, domain names, URI, IP addresses and DNS forms the corner stone
for identification/addressing and discovering associated data/devices related to
the identifier. 

## Preambule

Currently we have plethora of IoT technologies. Each using its own set of
identifiers, naming conventions, namespaces and process of discovering. The
problem that arises due to this is that a "thing" using one technology (e.g.
Zigbee protocol) will not be able to communicate with a "thing" using another
technology (e.g. WiFi). In simple terms, the problem is *"interoperability"*. 

An ideal solution would be that all of them move to a single technology, which is
also not possible. The reason, being each of the IoT technologies satisfies a
niche market. The task of interoperating with different technologies is possibly
taken care by gateways, which acts as a bridge.

The issue then arises is that, how to provision an identifier uniquely for a
thing in the Internet (which includes the IoT scope)? Provisioning of
identifiers in the IoT field is not well regulated as in the Internet. 

In the Internet, domain names and IP addresses have their own namespaces and are
managed in a hierarchical distributed manner. For e.g. for the IP addresses,
IANA allocates address space to RIRs (Regional Internet Registries), which in
turn distributes the allocated address space to LIRs (Local Internet
Registries), which in turn distributes to the end-users. Similarly for domain
names, we have ICANN, ccTLDs (country code Top Level Domains), gTLDs (generic
Top Level Domains) and then finally to the end-user. This manner of hierarchical
management makes sure that there is no duplicity and a particular IP address or
domain name is unique in the global Internet scope. 

Most of the so called IoT use cases does not use either IP addresses or domain
names for identifying a "thing". The following subsection shows two different
manners how IoT identifiers are structured:

### Hierarchical use-case in IoT

The first use-case is the identifier used in the supply chain market. The term
IoT was actually coined by this industry. The industry has been there well
before the Internet, and once the Internet has gained popularity, they wanted to
leverage the benefits of the Internet. 

EPC (Electronic Product Code) is the naming convention they use. The
barcodes attached to all the objects (e.g. water bottles, food items)  in the
consumer market follow the EPC naming convention. The organisation which
manages the allocation of EPC is called GS1. Their management hierarchy is
similar to IP or domain namespace allocation. There is GS1 global (like ICANN or
IANA) and there is one GS1 for most of the Countries in the world (For e.g. for
France, there is GS1 France). Each Country is allocated a batch or a single three
digit number. For e.g. all consumer products which has the EPC that starts
between 300 - 375, means it has been produced in France. 

The figure ![alt text](https://github.com/sandoche2k/ripe-iot/blob/master/images/Bar-code.png)
shows an example of a barcode attached to a product which has been produced in
France. This barcode is unique withing the GS1 namespace. 

### Flat use-case in IoT

UDID (Unique Device Identifier) is a unique serial number assigned to each Apple
manufactured device. It is a 40-character alphanumeric string of code as
follows:

```sh
2b6f0cc904d137be2e1730235f5664094b831186
```

UDID is used by Apple to track and record the Apple manufactured devices. It is
not hierarchical. The UDID is unique within the Apple UDID namespace. 

## Problem statement

The question that arises is how to integrate the different identifiers (either
flat or hierarchical) in to the Internet scope?

Two possible solutions seem to be :
   * Migrate all identifiers in IoT to use IPv6 addresses. 
   * Create a specific namespace in the Internet for each particular IoT usage.

The IETF (Internet Engineering Task Force) has been working for a while via
various IoT
[Working
Groups](https://www.internetsociety.org/blog/2017/07/rough-guide-to-ietf-99-internet-of-things/)
to make it possible to use IPv6 in the IoT devices. The operational issue is
that industries which has been using their own identifiers for a while are
reluctant to migrate to a new identifier. Just imagine, asking Wal-mart to put
IPv6 identifiers instead of barcode for identifying consumer goods.

Another possibility is to convert the existing identifier (either flat or
hierarchical) into a FQDN (Fully Qualified Domain Name) and then creating their
own namespace in the Internet. 

Provisioning both identifiers (discussed as use-cases above); the barcode and the
UDID could be included into the Internet via the DNS namespace as follows:

```sh
		.
	       / \
	      /   \
	     /	   \ 	
	    gs1    apple 
	     /\      \	
	    /  \      \
	  4.0.3	      UDID      
            /          \
           /            \
     6.2.3.3.9.3.     2b6f0cc904d137be2e1730235f5664094b831186 
	  /
	 /
      3.1.3.1
```

Then it is upto the client libraries to make the conversion and add the
sub-domain with respect to the identifiers. Once the identifier is converted to
a FQDN as follows : 

```sh
2b6f0cc904d137be2e1730235f5664094b83118.udid.apple. 
3.1.3.1.6.2.3.3.9.3.4.0.3.gs1. (supposing that there is a TLD called 'gs1')
```
they will follow the normal DNS resolution to resolve to its associated
resource/device/metadata. 


## Role for RIPE in the IoT domain

Since IoT is the Internet, with additional things associated with carrier
devices wanting to be interconnected, RIPE will play the same role as it does in
the Internet today. 

Many and many IoT applications and services will require the necessity to
interoperate. Some of them will see the advantages of migrating to IPv6, wherein
RIPE will play a role. Other well established industries (such as the Wal-mart
example described before) will use their existing identifiers, but will be
obliged to be part of the *Internet naming namespace.* 

Thus numbering and naming community will play an important role in the IoT. And,
it seems the upper echelons of both the numbering and naming community had
foreseen this by signing an [MoU
recently](https://www.ripe.net/publications/news/announcements/ripe-ncc-and-centr-sign-mou)
