# Quality attributes
Notes on quality attributes in information systems

There seems to be no consensus what so ever in the industry about quality attributes. Also known as non-functional requirements (NFRs) or service qualities. Therefore, I'll try to make up my own mind, and perhaps discover a modell. Which, like all other models, will be wrong, but some are usefull.

First two guidelines I have discovered to help slice and dice the model.

Number one, there are three domains to be considered;
1) The cyber domain (or information domain?) with three basic capabilities; store, move and process information.
2) The cyber-physical domain with two basic capabilities; input and output of information between the cyber and the physical domain. Sensors and actuators, DAC and ADC. Explicitly not including IO in a storage or communication devices this is considered as the "move" capability of the cyber domain. Side channel attackts lives in this domain.
3) The physical domain. Aka the rest of the universe, mostly out of scope for now.

Number two, there are three basic stakeholder roles to consider. The actual stakeholders may have one or more roles. I believe that the needs of these groups should be consistent across different systems. Like say owners or providers are never going to have a usability need with regard to the provided system. If so they are in the role of a user.
1) System owners.
2) System providers. Usually consisting of a vendor, DEV, OPS, SRE or if you work at Amazon or is some poor full-stack engineer named Brent (Phoenix Project joke), then you run it if you build it.
3) System users. The group that uses the system for the purposes of some subset of its functinal requirements.

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

I'd like to find some natural way to structure quality attributes such that they are more easily reasoned about and such that I can with greater certainty know if I have covered the whole spectrum. A hierarchical model, like TOGAF is attempting, would be nice because one could more easily identify areas to emphasize if you first know that a higher-level attribute is of importance to the system. However it is not certain that quality attributes naturally organises into som kind of a tree structure hierarchy.
https://www.youtube.com/watch?v=ARkLVvtxUZI
https://www.slideshare.net/Kevlin/a-system-is-not-a-tree

Example: you build a system that needs high availability. If your workload is variable, you will need to consider performance during peaks to ensure availability, and perhaps even scalability to handle large variations. The TOGAF model only partially helps in this scenario, listing performance as a subset of availability, but not scalability. This is a bit strange when you read the TOGAF definition of scalability.

I've long had this feeling that the sorry state of definitions of quality attributes is a major indicator of the IT-industry’s immaturity. So far into this note I'm not feeling better. How can an inconsistent model like the TOGAF "Taxonomy of service qualities" survive multiple revisions over two decades?

"Am I reinventing the wheel?" moment finally arrived after some digging around; Firesmith taxonomy (2003) ftp://ftp.cert.org/public/documents/03.reports/pdf/03tn033.pdf

---
random notes: higher level qualities; system should: evolve/cope with change, be trust wordy (secure), socially compliant (political legal ethical) usability, fits better with the cyber-physical domain than the "pure" cyber-domain. Can split model. clarify stakeholder roles.
