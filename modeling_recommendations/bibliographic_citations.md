Bibliographic Citations for Rare Materials Cataloging
=====================================================
RareMat, 2018-01-12

Table of Contents
> - [Overview](#overview)
> - [Entities to Be Modeled](#entities)
> - [Summary of Recommendations](#recommendations)
> - [Areas for Future Research](#future)
> - [Recommended Classes](#classes)
> - [Recommended Properties](#properties)
> - [Diagrams](#diagrams)


<a name="overview">Overview</a>
--------
Rare materials catalogers often cite reference sources listed in the Standard Citation Forms (SCF) database ([*https://rbms.info/scf/*](https://rbms.info/scf/)) to support the description and identification of particular items or editions. SCF entries can be thought of as authority records for individual reference sources, but they do not currently provide canonical work-level URIs for those sources. Sources are typically cited using a controlled string that identifies the source--for example, "Wing, D.G. Short-title catalogue of books printed in England, Scotland, Ireland, Wales, and British America, and of English books printed in other countries, 1641-1700 (2nd ed. 1994)"--often accompanied by a value that describes the location within the source where the item or edition being cataloged is referenced. Users should be able to query on both the reference source and the specific location of an entry within the source.

Additionally, there is a need to model "negative citations": catalogers will often cite a reference source in order to indicate that the item being cataloged is not listed in standard sources.

In total, there are four use cases to be modeled:
>1.  A citation is found, and the cataloger does not add commentary on the citation.
>2.  A citation is found, and the cataloger adds commentary on the citation.
>3.  A citation is not found, and the cataloger does not add commentary.
>4.  A citation is not found, and the cataloger adds further commentary about the reference source or a related citation.

There is also a need to model dates, identifiers, and other data related to citations. The proposed model will follow the general BIBFRAME modeling practices for dates, identifiers, and any other core data elements.

To address these four use cases, a new class should be created to represent bibliographic citation entities (**ex:Citation**). A citation functions as an intermediate node between a reference source, and a resource of interest to the cataloger (typically a bf:Item or bf:Instance).

A citation is related to a resource of interest by the property **ex:hasCitation** (inverse ex:isCitationOf) and to the citing work by the property **ex:hasSource** (inverse ex:isSourceOf).

A citation may link directly to its source, or it may link indirectly to the source through a specific location, modeled as a hierarchical chain proceeding from the most specific location up to the citing source. For example, a citation entity may be listed as a specific **ex:Entry** in a citing source, which may be located (**bf:place**) on a **ex:Page**, which may be part of (**bf:partOf**) a **ex:Volume**, which may be part of (**bf:partOf**) the citing source (**bf:Instance**).

Cataloger comments on citations are constructed using the BIBFRAME notes.

A negative citation is also modeled as an **bf:Note**, with the value "not found."

<a name="entities">Entities to Be Modeled</a>
----------------------
| Entity       | Type         | 
|:-------------|:-------------|
| Resource of interest to cataloger; typically instance or item but may also be a work | bf:Instance, bf:Item, bf:Work |
| Reference source    | bf:Instance, bf:Work      |
| Cataloger commentary | bf:Note      |
| Citation | ex:Citation     |

<a name="recommendations">Summary of Recommendations</a>
--------------------------

1.  Create a new class, **ex:Citation**, to represent bibliographic citations.

2.  Create a new property, **ex:hasCitation** (inverse ex:isCitationOf) to link a citation to a cited resource. 

2.  Optionally, the location within a citing source may also be specified. Create new classes, **ex:Volume**, **ex:Page**, and **ex:Entry**, to record the location of a citation.

3.  Consider other location designators as appropriate.

<a name="future">Areas for Future Research</a>
--------------------------
Earlier versions of this recommendation attempted differing levels of integration with the Citation Typing Ontology ([CiTO](http://www.sparontologies.net/ontologies/cito)), a [SPAR](http://www.sparontologies.net/) ontology focused on modeling citations. A second SPAR ontology, the Bibliographic Reference Ontology ([BiRO](http://www.sparontologies.net/ontologies/biro)), is also relevant to the bibliographic citations use case in RareMat. However, the precise relationship, if any, among RareMat citations, CiTO citations, and BiRO bibliographic references is an area that requires further research and clarification and lies beyond the scope of the current proposal.

<a name="classes">Recommended Classes</a>
-------------------

**ex:Citation**
> - **Label:** Citation
> - **URI:** http://example.org/Citation
> - **Subclass of**:
> - **Definition:** A single citation within a bibliographic source.
> - **Comment:**

**ex:Entry**
> - **Label:** Entry
> - **URI:** http://example.org/Entry
> - **Subclass of**:
> - **Definition:** A specific entry that locates a citation within a bibliographic source.
> - **Scope note:** Used in parsing out hierarchically structured location designators for citations.

**ex:Page**
> - **Label:** Page
> - **URI:** http://example.org/Page
> - **Subclass of**:
> - **Definition:** A single page within a resource.
> - **Comment:** Used in any page-level description, as well as in parsing out hierarchically structured location designators for citations.

**ex:Volume**
> - **Label:** Volume
> - **URI:** http://example.org/Volume
> - **Subclass of**:
> - **Definition:** A single bibliographic or physical volume of a resource.
> - **Comment:** Used in any volume-level description, as well as in parsing out hierarchically structured location designators for citations.


<a name="properties">Recommended Properties</a>
----------------------

**bf:place**
> - **Label:** Place
> - **URI:** [*http://id.loc.gov/ontologies/bibframe/place*](http://id.loc.gov/ontologies/bibframe/place)
> - **Domain:** Unspecified
> - **Range:** http://id.loc.gov/ontologies/bibframe/Place
> - **Definition:** Geographic location or place entity associated with a resource or element of description, such as the place associated with the publication, printing, distribution, issue, release or production of a resource, place of an event.

**ex:hasSource**
> - **Label:** has source
> - **URI:** [*http://example.org/hasSource*](http://example.org/hasSource)
> - **Domain:** Unspecified
> - **Range:** Unspecified
> - **Inverse:** ex:isSourceOf
> - **Definition:** Relates this resource to the source from which it was derived.

**ex:hasCitation**
> - **Label:** has citation
> - **URI:** [*http://example.org/hasCitation*](http://example.org/hasCitation)
> - **Domain:** Unspecified
> - **Range:** Unspecified
> - **Inverse:** ex:isCitationOf
> - **Definition:** The resource that is the focus of description (e.g., a bf:Item or bf:Instance) has a citation located in a standard reference source.

**bf:partOf**
> - **Label:** Is Part Of
> - **URI:** [*http://id.loc.gov/ontologies/bibframe/hasPart*](http://id.loc.gov/ontologies/bibframe/hasPart)
> - **Definition:** Resource that is included either physically or logically in the described resource


<a name="diagrams">Diagrams</a>
--------

### Use case 1: Basic citation.
![Use Case 1](/modeling_recommendations/modeling_diagrams/citation_basic.png)

### Use case 2: Citation located, cataloger adds commentary on citation.
![Use Case 2](/modeling_recommendations/modeling_diagrams/citation_with_note.png)

### Use case 3: Negative citation (without comment).
![Use Case 3](/modeling_recommendations/modeling_diagrams/citation_negative.png)

### Use case 4: Negative citation with comment.
![Use Case 4.1](/modeling_recommendations/modeling_diagrams/citation_negative_with_note.png)
