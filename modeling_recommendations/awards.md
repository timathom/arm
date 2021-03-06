Awards
================
ArtFrame, 2017-11-17

Summary Recommendation 
-----------------------

Table of Contents
> - [Overview](#overview)
> - [Awards in BIBFRAME](#bfawards)
> - [Recommendations for Moving Forward](#recommendations)
> - [Diagram](#diagram)
> - [Examples](#examples)


--------

Many artists, artworks or art related publications represented in our library collections are recipients of awards. 
Being able to find all the resources connected to a specific award within one collection or across different collections 
has been identified as a critical use case ([*https://wiki.duraspace.org/display/LD4P/ArtFrame?preview=/79795202/83235173/PublicUseCases.pdf*](https://wiki.duraspace.org/display/LD4P/ArtFrame?preview=/79795202/83235173/PublicUseCases.pdf))by the ArtFrame group. An award could be given to a creator for a specific work 
(in which case the award would need to be associated with that work) or it could be a career achievement award that can only 
be associated with the agent, but not with a specific work.

The ArtFrame group considered the inclusion of awards in the LD4P event model (tbd), but decided that for the ArtFrame use case 
the actual event, e.g. an awards ceremony, is not what is considered important. It is sufficient to say that a specific work or 
agent received a specific award on a given date.

In the traditional MARC environment, catalogers have recorded award information in the Awards note: 586. ([*http://www.loc.gov/marc/bibliographic/bd586.html*](http://www.loc.gov/marc/bibliographic/bd586.html)) Access points related 
to awards are generally coded as LC subject headings (150 with a 550 Art--Awards), however these LCSH terms are applied to 
resources about that award, not to those receiving an award. The content standard RDA covers awards in 7.28. The instructions 
are limited to “Record information on an award if considered important for identification or selection.” The examples reflect a 
note style. The RDA registry provides a property rdau:P60090. ([*http://metadataregistry.org/schemaprop/show/id/14686.html*](http://metadataregistry.org/schemaprop/show/id/14686.html))

In BIBFRAME a property bf:awards is available. However, bf:awards is a datatype property and therefore carries the MARC practice 
forward to record related information in a text string. It does currently not allow for linking out to awards, for example in 
Wikidata (e.g. Sobey Art Award) ([*https://www.wikidata.org/wiki/Q7549952*](https://www.wikidata.org/wiki/Q7549952)).
The VIVO ontology has a class vivo:Award ([*http://vivoweb.org/sites/vivoweb.org/files/vivo-isf-public-1.6.owl#Award*](http://vivoweb.org/sites/vivoweb.org/files/vivo-isf-public-1.6.owl#Award))and related properties, however those tend to have ranges limiting their use to foaf:Agent or foaf:Organization.

The art specific standards and ontologies that were investigated do not specifically address the issue of awards.

While the awards model was developed specifically to address the descriptive needs of bibliographic items in the art and rare materials domains, we define it as an independent model with the expectation that it could be useful in the description of awards related to a broad range of resources.


<a name="bfawards">Awards in BIBFRAME</a>
============
Properties
---------
**bf:awards**
> - **Label**: Award note
> - **URI**: http://id.loc.gov/ontologies/bibframe/awards
> - **Definition**: Information on awards associated with the described resource.
> - **Used with**: Work or Instance
> - **Range**: Literal

<a name="recommendations">Recommendations</a>
===========================

The proposed Award model for ArtFrame is in part based on the award classes and properties developed for the LD4L 2014 Ontology ([*https://www.ld4l.org/ld4l-2014/ontology*](https://www.ld4l.org/ld4l-2014/ontology)) and a proposal developed for bibliotek-o that remained unfinished due to time constraint. However, these models were adjusted and extended to accommodate use cases and data examples identified by the ArtFrame group.

Classes
---------
**Award**
> - **Label**: Award or Honor
> - **URI**: http://vivoweb.org/ontology/core#Award
> - **Definition**: An award or honor

**Activity**
> - **Label**: Activity
> - **URI**: http://example.org/Activity
> - **Definition**: An activity or contribution by a single agent that affects or alters the existence or state of a resource.

**AwardSelectorActivity**
> - **Label**: Award selector
> - **URI**: http://award.example.org/AwardSelectorActivity
> - **Definition**: The activity of nominating or judging a resource in relation to an award, honor, etc.
> - **scopeNote**: This class is not derived from a MARC relator.
> - **Subclass of**: ex:Activity

**AwardGranterActivity**
> - **Label**: Award granter
> - **URI**: http://award.example.org/AwardGranterActivity
> - **Definition**: The activity of granting an award.
> - **scopeNote**: This class is not derived from a MARC relator.
> - **Subclass of**: ex:Activity

**AwardReceipt**
> - **Label**: Award receipt
> - **URI**: http://award.example.org/AwardReceipt
> - **Definition**: The bestowal of an award, honor, or distinction to an Agent or Work. The award bestowed should be represented with the Award class. The AwardReceipt is a context node between the award and the recipient which may contain further information, such as date.

**AwardWinner**
> - **Label**: Award winner
> - **URI**: http://award.example.org/AwardWinner
> - **Definition**: The specific nature of the award receipt is award winner.
> - **Subclass of**: award:AwardReceipt

**AwardShortlist**
> - **Label**: Award shortlist
> - **URI**: http://award.example.org/AwardShortlist
> - **Definition**: The specific nature of the award receipt is award shortlist.
> - **Subclass of**: award:AwardReceipt

**AwardHonoraryMention**
> - **Label**: Award honorary mention
> - **URI**: http://award.example.org/AwardHonoraryMention
> - **Definition**: The specific nature of the award receipt is honorary mention.
> - **Subclass of**: award:AwardReceipt

**AwardNominee**
> - **Label**: Award nominee
> - **URI**: http://award.example.org/AwardNominee
> - **Definition**: The specific nature of the award receipt is nominee.
> - **Subclass of**: award:AwardReceipt

**AwardCitation**
> - **Label**: Award citation
> - **URI**: http://award.example.org/AwardCitation
> - **Definition**: The specific nature of the award receipt is citation.
> - **Subclass of**: award:AwardReceipt

**AwardLonglist**
> - **Label**: Award longlist
> - **URI**: http://award.example.org/AwardLonglist
> - **Definition**: The specific nature of the award receipt is longlist.
> - **Subclass of**: award:AwardReceipt

Properties
---------
**receives (object property)**
> - **Label**: receives
> - **URI**: http://award.example.org/receives
> - **Definition**: This resource, such as an Agent or Work, is the recipient of the specified AwardReceipt
> - **Domain**: unspecified
> - **Inverse**: award:receivedBy
> - **Range**: award:AwardReceipt

**receivedBy (object property)**
> - **Label**: received by
> - **URI**: http://award.example.org/receivedBy
> - **Definition**: This AwardReceipt was received by the specified award recipient (such as an Agent or Work).
> - **Domain**: award:AwardReceipt
> - **Range**: unspecified
> - **Inverse**: award:receives

**hasAward (object property)**
> - **Label**: has award
> - **URI**: http://award.example.org/hasAward
> - **Definition**: This resource is a receipt of the specified award or honor.
> - **Domain**: award:AwardReceipt
> - **Range**: award:Award
> - **Inverse**: award:isAwardOf

**isAwardOf (object property)**
> - **Label**: is award of
> - **URI**: http://award.example.org/isAwardOf
> - **Definition**: Links a specified award or honor to its receipt.
> - **Domain**: award:Award
> - **Range**: award:AwardReceipt
> - **Inverse**: award:hasAward

**bf:date**
> - **Label**: Date
> - **URI**: http://id.loc.gov/ontologies/bibframe/date
> - **Definition**: Date designation associated with a resource or element of description, such as date of title variation; year a degree was awarded; date associated with the publication, printing, distribution, issue, release or production of a resource. May be date typed.

**bf:agent (Object property)**
> - **Label**: Associated agent
> - **URI**: http://id.loc.gov/ontologies/bibframe/agent
> - **Definition**: Entity associated with a resource or element of description, such as the name of the entity responsible for the content or of the publication, printing, distribution, issue, release or production of a resource.
> - **Domain**: bf:Agent

**agentOf (Object property)**
> - **Label**: agent of
> - **URI**: http://example.org/agentOf
> - **Definition**: Relates an Agent to an Activity they participated in.
> - **Inverse**: bf:agent

**hasActivity (Object property)**
> - **Label**: has activity
> - **URI**: http://example.org/hasActivity
> - **Definition**: Relates this resource to an activity or contribution by a single agent that affects or alters its existence or state.
> - **Inverse**: ex:isActivityOf

**isActivityOf (Object property)**
> - **Label**: is activity of
> - **URI**: http://example.org/isActivityOf
> - **Definition**: Relates an activity to the affected resource.
> - **Inverse**: ex:hasActivity

<a name="Diagram">Diagram</a>
===========

![Award model diagram](/modeling_recommendations/modeling_diagrams/award.png)

<a name="examples">Examples</a>
--------

> - **586 (awards note): Man Booker Prize, 1987, shortlist -- BIBFRAME**
```

:w1 a bf:Work ;
bf:awards "Man Booker Prize, 1987, shortlist" .

```
> - **586 (awards note): Man Booker Prize, 1987, shortlist -- biblioteko/ArtFrame**
```
:chatterton a bf:Work ;
 award:receives :awardReceipt1 .

:awardReceipt1 a af:AwardReceipt, af:AwardShortlist ;
 award:hasAward :award1 ;
 award:receivedBy :chatterton ;
 award:date "1987" .

:award1 a vivo:Award ;
 rdfs:label "Man Booker Prize" .

```
> - **586 (awards note): George Wittenborn Award, Art Libraries Society of North  America, 1998 -- BIBFRAME**
```
w1 a bf:Work ;
bf:awards "George Wittenborn Award, Art Libraries Society of North  America, 1998" .

```
> - **586 (awards note): George Wittenborn Award, Art Libraries Society of North  America, 1998 -- biblioteko/ArtFrame**
```
:Ikat a bf:Work ;
 award:receives :awardReceipt1 .

:awardReceipt1 a award:AwardReceipt, award:AwardWinner  ;
 award:hasAward :award1 ;
 award:receivedBy :Ikat ;
 bf:date "1998" ;
 ex:hasActivity :activity1 .

:award1 a vivo:Award ;
 rdfs:label "George Wittenborn Award" .

:activity1 a award:AwardGranterActivity ;
 bf:agent <http://id.loc.gov/row/agents/n82039281> .

```
> - **586 (awards note): Smith Award, Decorative Arts Society, 2006, for the essay,  "The most artistic house in New York City" -- BIBFRAME**
```
w1 a bf:Work ;
bf:title :t1 ;
bf:partOf :w2 ;
bf:awards "Smith Award, Decorative Arts Society, 2006” .

:t1 a bf:Title ;
rdfs:label "The most artistic house in New York City" ;
bf:mainTitle "The most artistic house in New York City" .

:w2 a bf:Work ;
bf:title :t2 ;
bf:hasPart :W1 .

:t2 a bf:Title ;
rdfs:label "Louis Comfort Tiffany and Laurelton Hall" ;
bf:mainTitle "Louis Comfort Tiffany and Laurelton Hall" .

```
> - **586 (awards note): Smith Award, Decorative Arts Society, 2006, for the essay,  "The most artistic house in New York City" -- biblioteko/ArtFrame**
```
:w1 a bf:Work ;
 bf:partOf :w2 ;
 award:receives :awardReceipt1 .

:awardReceipt1 a award:AwardReceipt, award:AwardWinner ;
 award:hasAward :award2 ;
 award:receivedBy :w1 ;
 bf:date "2006" ;
 ex:hasActivity :activity1 .
 
:award2 a vivo:Award ;
 rdfs:label "Smith Award" .

:activity1 a award:AwardGranterActivity ;
 bf:agent :agent1 .

:agent1 a bf:Organization ;
 rdfs:label "Decorative Arts Society" .

```
> - **Someone talked! (Poster) "Winner R. Hoe & Co., Inc. Award - National War Poster Competition. -- BIBFRAME**
```
:w a bf:Work ;
bf:award "Winner R. Hoe & Co., Inc. Award - National War Poster Competition."

```
> - **Someone talked! (Poster) "Winner R. Hoe & Co., Inc. Award - National War Poster Competition. -- biblioteko/ArtFrame**
```
:SomeoneTalked! a bf:Work ;
 award:receives :awardReceipt1 .

:awardReceipt1 a award:AwardReceipt, award:AwardWinner ;
 award:hasAward :award1 ;
 award:receivedBy :SomeoneTalked! .

:award1 a vivo:Award ;
 rdfs:label "R. Hoe & Co., Inc. Award--National War Poster Competition" .

```
> - **Award selector/judge -- biblioteko/ArtFrame**
```
:MurrayHill a bf:Person ;
 award:receives :awardReceipt.

:awardReceipt a award:AwardReceipt, a award:AwardWinner ;
 award:isReceiptOf :AnnualContemporaryCrafExhibitionforGlass ;
 award:receivedBy :MurrayHill ;
 bf:date "1987" ;
 ex:hasActivity :activity1, :activity2 .

:activity1 a award:SelectorActivity ;
 bf:agent <http://id.loc.gov/row/agents/no2003101967> .

:activity2 a award:AwardGranterActivity ;
 bf:agent :agent2 .
