# Quality attributes
Notes on quality attributes in information systems

https://www.xkcd.com/2030/
https://www.xkcd.com/2021/

There seems to be no consensus what so ever in the industry about quality attributes. Also known as non-functional requirements (NFRs) or service qualities. Therefore, I'll try to make up my own mind, and perhaps discover a model. Which, like all other models, will be wrong, but some are useful.

First two guidelines I have discovered to help slice and dice the model.

Number one, there are three domains to be considered;
1) The cyber domain (or information domain?) with the three elements of computation; processing, storage and communcation. https://www.youtube.com/watch?v=7erJ1DV_Tlo
2) The cyber-physical domain with two basic capabilities; input and output of information between the cyber and the physical domain. Sensors and actuators, DAC and ADC. Explicitly not including IO in a storage or communication device, as this is considered the "move" capability of the cyber domain. Side channel attacks lives in this domain.
3) The physical domain. Aka the rest of the universe, mostly out of scope for now.

Number two, there are three basic stakeholder roles to consider. The actual stakeholders may have one or more roles, but the existence of these three roles should be consistent across all systems, so be sure to cover them all. Quality attributes exists in relation between stakeholders and the system. Therefore, it is key to have a consistent model for stakeholders in order to create a consistent model for quality attributes across all types of systems.

1) System owners.
2) System providers. Usually consisting of a vendor, DEV, OPS, SRE or if you work at Amazon or is some poor full-stack engineer named Brent (Phoenix Project joke), then you run it if you build it.
3) System users. The group that uses the system for the purposes of some subset of its functional requirements.

# Enumerating and structuring quality attributes

TOGAF provides a structured view of Quality attributes, however it seems to be in conflict with the Parkerian Hexad definition of security. The same goes for the more frequently used, but probably insufficient, CIA-triad definition of security.

Listing some quality attributes subsets

### CIA-triad, security is a set of:
- Confidentiality
- Integrity
- Availability

### Parkerian Hexad (1998), security is a set of:
https://en.wikipedia.org/wiki/Parkerian_Hexad
- Confidentiality
- Possession or Control
- Integrity
- Authenticity
- Availability
- Utility

### TOGAF Application Platform Service Qualities (1998):
http://www.opengroup.org/public/arch/p3/trm/tx/tx_quals.htm (1998)
http://pubs.opengroup.org/architecture/togaf8-doc/arch/chap19.html (2006) unchanged
http://pubs.opengroup.org/architecture/togaf91-doc/arch/chap43.html 43.4.3.2 Taxonomy of Service Qualities, TOGAF 9.1 unchanged

##### Availability (the degree to which something is available for use), including:
* manageability, the ability to gather information about the state of something and to control it
* serviceability, the ability to identify problems and take corrective action such as torepair or upgrade a component in a running system
* performance, the ability of a component to perform its tasks in an appropriate time
* reliability, or resistance to failure
* recoverability, or the ability to restore a system to a working state after an interruption
* locatability, the ability of a system to be found when needed
##### Assurance, including:
* security, or the protection of information from unauthorized access
* integrity, or the assurance that data has not been corrupted
* credibility, or the level of trust in the integrity of the system and its data
##### Usability, or ease of operation by users, including:
* International operation, including multilingual and multicultural abilities
##### Adaptability, including:
* interoperability, whether within or outside the organization (for instance interoperability of calendaring or scheduling functions may be key to the usefulness of a system)
* scalability, the ability of a component to grow or shrink its performance or capacity appropriately to the demands of the environment in which it operates
* portability, of data, people, applications, and components
* extensibility, or the ability to accept new functionality
* the ability to offer access to services in new paradigms such as object orientation.

Reference:
List of NFRs on Wikipedia:
https://en.wikipedia.org/wiki/Non-functional_requirement

TOGAF has a definition of security that reads more like confidentiality, which is considered a subset of security by most definitions.

I'd like to find some natural way to structure quality attributes such that they are more easily reasoned about and such that I can with greater certainty know if I have covered the whole spectrum. A hierarchical model, like TOGAF is attempting, would be nice because one could more easily identify areas to emphasize if you first know that a higher-level attribute is of importance to the system. However, it is not certain that quality attributes naturally organizes into some kind of a tree structure hierarchy.
https://www.youtube.com/watch?v=ARkLVvtxUZI
https://www.slideshare.net/Kevlin/a-system-is-not-a-tree

Example: you build a system that needs high availability. If your workload is variable, you will need to consider performance during peaks to ensure availability, and perhaps even scalability to handle large variations. The TOGAF model only partially helps in this scenario, listing performance as a subset of availability, but not scalability. This is a bit strange when you read the TOGAF definition of scalability.

I've long had this feeling that the sorry state of definitions of quality attributes is a major indicator of the IT-industry’s immaturity. So far into this note I'm not feeling better. How can an inconsistent model like the TOGAF "Taxonomy of service qualities" survive multiple revisions over two decades?

"Am I reinventing the wheel?" moment finally arrived after some digging around; Firesmith taxonomy (2003) ftp://ftp.cert.org/public/documents/03.reports/pdf/03tn033.pdf

### Firesmith taxonomy:

#### Development-oriented quality factors
are quality factors that are primarily important
during development and maintenance rather than usage. Examples of development-oriented
quality factors and subfactors include the following:
##### Maintainability
is the ease with which an application or component can be maintained
between major releases. Maintainability includes the following quality subfactors:
* Correctability is the ease with which minor defects can be corrected between major
releases while the application or component is in use by its users.
* Extensibility is the ease with which an application or component can be enhanced in
the future to meet changing requirements or goals.
##### Portability
is the ease with which an application or component can be moved from one
environment to another.
##### Reusability
is the ease with which an existing application or component can be reused.
##### Scalability
is the ease with which an application or component can be modified to
expand its existing capacities.
##### Verifiability
is the ease with which an application or component can be verified to meet
its associated requirements and standards. Verifiability includes the following subfactor:
* Testability is the ease with which an application or component facilitates the
creation and execution of successful tests (i.e., tests that would cause failures due to
any underlying defects). 

#### Usage-oriented quality factors
are quality factors that are primarily important after
deployment and during actual usage of an application or component. Examples of usageoriented
quality factors and subfactors include the following:
##### Auditability
is the degree to which sufficient records are kept to support a financial
audit.
##### Branding
is the degree to which a work product (e.g., application, component, or
document) successfully incorporates the brand of the customer organization’s business
enterprise.
##### Capacity
is the minimum number of things (e.g., transactions, storage) that can be
successfully handled.
##### Configurability
is the degree to which something can be configured into multiple forms
(i.e., configurations). Configurability includes the following quality subfactors:
* Internationalization (also known as globalization and localization) is the degree to
which something can be or is appropriately configured for use in a global
environment.
* Personalization is the degree to which each individual user can be presented with a
unique user-specific experience.
* Subsetability is the degree to which something can be released in multiple variants,
each of which implements a different subset of the functional requirements and
associated quality requirements.
* Variability is the degree to which something exists in multiple variants, each having
the appropriate capabilities.
##### Correctness
is the degree to which a work product and its outputs are free from defects
once the work product is delivered. Correctness includes the following quality subfactors:
* Accuracy is the magnitude of defects (i.e., the deviation of the actual or average
measurements from their true value) in quantitative data.
* Currency is the degree to which data remain current (i.e., up to date, not obsolete).
* Precision is the dispersion of quantitative data, regardless of its accuracy.
##### Dependability
is the degree to which various kinds of users can depend on a work
product. Dependability includes the following quality factors: 
* Availability is the degree to which a work product is operational and available for
use.
The issue of availability is a difficult one for any quality model that seeks to
minimize the overlap of quality factors in its taxonomy. When systems and software
engineers think of availability requirements, they think in terms of non-malicious
causes of lack of availability. However, a denial-of-service (DoS) attack is clearly a
security problem. To maintain the disjointed nature of the taxonomy of quality
factors, the scope of availability will remain non-malicious and DoS will be dealt
with as a violation of a type of security requirements.
* Reliability is the degree to which a work product operates without failure under
given conditions during a given time period.
* Robustness is the degree to which an executable work product continues to function
properly under abnormal conditions or circumstances. Robustness includes the
following quality subfactors:
* Environmental tolerance is the degree to which an executable work product
continues to function properly despite existing in an abnormal environment.
* Error tolerance is the degree to which an executable work product continues to
function properly despite the presence of erroneous input.
* Failure tolerance is the degree to which an executable work product continues
to function properly despite the occurrence of failures, where
* A failure is the execution of a defect that causes an inconsistency between an
executable work product’s actual (observed) and expected (specified)
behavior.
* A defect may or may not cause a failure depending on whether the defect is
executed and whether exception handling prevents the failure from
occurring.
* A fault (also known as defect, bug) is an underlying flaw in a work product
(i.e., a work product that is inconsistent with its requirements, policies, goals,
or the reasonable expectations of its customers or users). Defects are
typically caused by human errors, and defects have no impact until they
cause one or more failures.
Failure tolerance includes the following quality subfactor:
* Fault tolerance is the degree to which an executable work product continues
to function properly despite the presence or execution of defects.
* Safety is the degree to which accidental harm is prevented, reduced, and properly
reacted to.
* Security is the degree to which malicious harm is prevented, reduced, and properly
reacted to.
The term “malicious” is used intentionally to clearly differentiate safety from
security and thereby avoid an unnecessary overlap in the taxonomy of quality factors.
Thus, safety deals with accidents, whereas security deals with attacks. However,
accidents (safety) can result in security vulnerabilities that can be exploited by 
attacks, at which time their consequences fall within the realm of security. Similarly,
attacks may cause safety hazards that in turn may cause accidents.
* Survivability is the degree to which essential, mission-critical services continue to
be provided in spite of either accidental or malicious harm.
##### Efficiency
is the degree to which something effectively uses (i.e., minimizes its
consumption of) its resources. These resources may include all types of resources such as
computing (hardware, software, and network), machinery, facilities, and personnel.
##### Interoperability
is the degree to which a system or one of its components is properly
connected to and operates with something else.
##### Operational
environment compatibility is the degree to which a system or a
component can be used and functions correctly under specified conditions of the physical
environment(s) in which it is intended to operate.
##### Performance
is the degree to which timing characteristics are adequate. Performance
includes the following quality subfactors:
* Jitter is the precision (i.e., variability) of the time when one or more events occur.
* Latency is the time it takes to provide a requested service or allow access to a
resource.
* Response time is the time it takes to initially respond to a request for a service or to
access a resource.
* Scheduleability is the degree to which events and behaviors can be scheduled and
then occur at their scheduled times.
* Throughput is the number of times that a service can be provided within a specified
unit of time.
##### Utility
is the degree to which something can be accessed and used by its various types of
users. Utility includes (but is not limited to) the following subfactors:
* Accessibility is the degree to which the user interface of something enables users
with common or specified (e.g., auditory, visual, physical, or cognitive) disabilities to
perform their specified tasks.
* Installability is the ease with which something can be successfully installed in its
production environment(s).
* Operability is the degree to which something enables its operators to perform their
tasks in accordance with the operations manual.
* Transportability is the ease with which something can be physically moved from
one location to another.
* Usability is the ease with which members of a specified set of users are able to use
something effectively. 
* Withdrawability is the ease with which an existing problematic version of the
system or one of its components can be successfully withdrawn and replaced by a
previously working version.

---
#### Notes on Firesmith Taxonomy
* has notion of developer and user stakeholders, not owner. "developer" seems like å less accurate definition than provider, as i lacks the notion of operations or SRE.
* the usage-oriented quality factor "correctness" has a sub factor "currency" which definition is resembling the C in CAP theorem, Consistency, or degree of consistency. Eventual consistency. This indicates that Partition tolerance should be considered as a quality attribute, at least for a distributed system. The availability definition in CAP seems much more specific than the definitions common in other models.
* configurability. Does versioning fit here?
* dependability, as a top-level description above availability is interesting. can it include the notion of anti-fragility and its requirement, diversity?

---

#### The many meanings of availability

Availability is one of the most common factors in lists and models of system behavior.

It is considered part of security in the CIA-triad and the Parkerian Hexad. It is considered a "higher level goal" in TOGAF, encapsulating capabilities that will make it possible to maintain availability over time. We find it in the more system state focused space of the CAP-theorem. And all the way down to the RAS and RAS+M meme like lists of system attributes used to sell expensive hardware. The definition of availability range from very strict in the CAP-theorem and Parkerian Hexad to less strict in most of the other definitions and all the way down to the TOGAF definition which is just circular; "Availability (the degree to which something is available for use)"

http://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html

Availability in CAP is defined as “every request received by a non-failing [database] node in the system must result in a [non-error] response”. It’s not sufficient for some node to be able to handle the request: any non-failing node needs to be able to handle it. Many so-called “highly available” (i.e. low downtime) systems actually do not meet this definition of availability.

Availability in the CAP theorem as explained by Martin Kleppmann. The definition also seems reasonable for stateless components. The major difference being that stateless distributed systems needs fewer external dependencies and therefore can have fewer failure modes.

One problem with this definition of availability is that it does not have a notion of time. The appropriate response time will greatly vary between systems. Ranging from very long if you are interacting with outer space entities like the Mars rover, or very low if you are doing something on-chip, like reading from a CPU registry. Sometimes we se expressions like "in a timely manner". Being guaranteed a response but not when to get it is often not good enough to meet typical expectations of availability. Gil Tene of Azul systems has some nice interviewing techniques to lure out the actual expectations to a system with regard to response times. First asking about the "typical response time" and then the worst case response time. usually getting a vague response for the max he answers back that the customer accepts [some extremely long response time with regards to the system]. Whereas the customer typically replies with a very low max response time that could make the system excessively expensive, at least in modern systems with very high technology stacks full of costly abstractions and noisy resource sharing.

#### The false dichotomy of functional and non-functional requirements.

Or perhaps the inadequate non-description of non-functional requirements. It seems like a better model is to divide requirements into three, perhaps four categories; Functional, (and then the "NFRs") Social, Security and perhaps lastly Operability or maintainability, covering the abilities to keep the system functioning through time and change.

Social requirements can again be divided into Status, legal and ethical requirements. Typically held by the stakeholders with the owner role. Although the programmer's oath by "uncle Bob" Martin claims that the stakeholders with the provider role (typically dev and ops) should hold these requirements as well.

https://blog.cleancoder.com/uncle-bob/2015/11/18/TheProgrammersOath.html

---
random notes, these will likely not make sense to you:
* higher level qualities; system should: evolve/cope with change, be trust wordy (secure), socially compliant (political legal ethical) usability, fits better with the cyber-physical domain than the "pure" cyber-domain. Can split model.
* clarify stakeholder roles.
* Look into quality attributes in relation to OODA-loops, and OODA lops in relation to Cynefin framework.
* vision, strategy, tactics, metrics. where does quality attributes fit in?
* Proposal; The systems quality attributes can be described as a connected graph of cascading intent (Stephen Bungay - The art of action) or promises (Mark Burgess - promise theory).
* this might become a wardley map(?) functional requirements (user needs) being the anchor.
TODO: https://www.fi.upm.es/catedra-ibmrational/sites/www.fi.upm.es.catedra-ibmrational/files/calero2.pdf

Quality attributes expressed as cost

* Reliable - Cost of failure
* Maintainable - Cost of change 
* Scalable - Cost of growth (subset of change? change in workload)
* Security - Cost of harm? (subset of reliable?)

ISO 25010:2011
https://webstore.iec.ch/preview/info_isoiec25010%7Bed1.0%7Den.pdf
http://adcorsi.com/analisidisegnowp/wp-content/uploads/2013/08/iso25010-en.pdf
serverless
https://www2.eecs.berkeley.edu/Pubs/TechRpts/2019/EECS-2019-3.pdf
