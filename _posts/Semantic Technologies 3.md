---
title: Semantic Technologies 1
date: 2018-04-01 15:19:45
tags:
- Reasoning
---

# Semantic Technologies 3
# Lecture 5 - 명제 기호 정리
# Lecture 6
## Syntactic reasoning
- We therefore need means to decide entailment syntactically:
	- Syntactic methods operate only on the form of a statement
	- syntactic reasoning is, in other words, computation.
- Syntactic reasoning easier to understand and use than model semantics
- - - -

## RDF Schema
- RDF Schema is a vocabulary defined by W3C.
Namespace:
rdfs: http://www.w3.org/2000/01/rdf-schema#
- Originally though of as a “schema language” like XML Schema.
- Comes with some inference rules
- A very simple modeling language
- and (for our purposes) a subset of OWL.

## RDF Schema Concept
- RDFS adds the concept of “classes” which are like types or sets of resources.
- The RDFS vocabulary allows statements about classes.
- Defined resources:
	**rdfs:Resource**: The class of resources, everything.
	**rdfs:Class**: The class of classes.
	**rdf:Property**: The class of properties (from rdf).
- Defined properties:
	**rdf:type**: relate resources to classes they are members of.
	**rdfs:domain**: The domain of a relation.
	**rdfs:range**: The range of a relation.
	**rdfs:subClassOf**: Class inclusion.
	**rdfs:subPropertyOf**: Property inclusion.


![](Semantic%20Technologies%203/6D760EEE-2BB9-45AE-92FC-2C37F2D245B2.png)


![](Semantic%20Technologies%203/D6B8C770-426B-4A12-A83D-E21264D22587.png)

## RDFS reasoning
RDFS supports three principal kinds of reasoning pattern:
1. **Type** propagation:
“The 2CV is a car, and a car is a motorised vehicle, so. . . ”
2. **Property** inheritance:
“Steve lectures at Ifi, and anyone who does so is employed by Ifi, so. . . ”
3. **Domain and range** reasoning:
“Everything someone has written is a document. Alan has written a book, therefore. . . ”
“All fathers of people are males. James is the father of Karl, therefore. . . ”

## Type propagation with rdfs:subClassOf
The type propagation rules apply
	- to combinations of rdf:type, rdfs:subClassOf and rdfs:Class,
	- and trigger recursive inheritance in a class taxonomy.

![](Semantic%20Technologies%203/6CC3CB00-51A6-4371-A49B-970B3B85DC0E.png)

![](Semantic%20Technologies%203/DD1973F1-477F-4484-8F70-112EF9A4FBA6.png)

### Example 
__RDFS/RDF knowledge base:__
ex:Vertebrate rdf:type rdfs:Class .
ex:Mammal rdf:type rdfs:Class .
ex:KillerWhale rdf:type rdfs:Class .
ex:Mammal rdfs:subClassOf ex:Vertebrate .
ex:KillerWhale rdfs:subClassOf ex:Mammal .
ex:Keiko rdf:type ex:KillerWhale .
__Inferred triples:__
ex:Keiko rdf:type ex:Mammal . (rdfs9)
ex:Keiko rdf:type ex:Vertebrate . (rdfs9)
ex:KillerWhale rdfs:subClassOf ex:Vertebrate . (rdfs11)
ex:Mammal rdfs:subClassOf ex:Mammal . (rdfs10)

![](Semantic%20Technologies%203/41C2A340-4BE3-4574-80C9-49582991D1C8.png)

## Multiple Inheritance
Similarly, a class is usually a subclass of many other classes.
![](Semantic%20Technologies%203/13046384-974E-4C7D-81C1-06609A22BC48.png)

## Second: Property transfer with rdfs:subPropertyOf
Reasoning with properties depends on certain combinations of
	- rdfs:subPropertyOf,
	- rdf:type, and
	- rdf:Property

![](Semantic%20Technologies%203/7C67901C-021E-48F6-9609-F1C44ECEEAEF.png)
![](Semantic%20Technologies%203/A16B4C0F-4603-422A-9A5C-174EF040D38F.png)

### Example

![](Semantic%20Technologies%203/BBD68B0F-6F8A-488E-B620-F439169CA8AA.png)

![](Semantic%20Technologies%203/61F28A43-0AD7-4E61-9B3F-239FD2C7C65B.png)

## Third pattern: Typing data based on their use
Triggered by combinations of
	- rdfs:range
	- rdfs:domain
	- rdf:type

![](Semantic%20Technologies%203/ECAB392D-7F36-492E-A882-A3DBEB81063D.png)

### Example
Suppose we have a class tree that includes:
	:SymphonyOrchestra rdfs:subClassOf :Ensemble .
and a property :conductor whose domain and range are:
	:conductor rdfs:domain :SymphonyOrchestra .
	:conductor rdfs:range :Person .
Now, if we assert	
	:OsloPhilharmonic :conductor :Petrenko .
we may infer;
	:OsloPhilharmonic rdf:type :SymphonyOrchestra .
	:OsloPhilharmonic rdf:type:Ensemble .
	:Petrenko rdf:type :Person .

![](Semantic%20Technologies%203/DE166FA7-BEC1-416A-90C3-C1C5649CA8E3.png)

## Ramification
This fact has two important consequences:
1.  RDFS is useless for validation,
... understood as sorting conformant from non-conformant documents,
since it never signals an inconsistency in the data,
it just goes along with anything,
and adds triples whenever they are inferred.
2. RDFS has no notion of negation at all
For instance, the two triples
	ex:Joe rdf:type ex:Smoker .,
	ex:Joe rdf:type ex:NonSmoker .
are not inconsistent.

## Conclusion
RDFS reasoners usually implement only the standardised incomplete rules, 
	so they do not guarantee complete reasoning.
Better therefore;
	if all you need is the three RDFS reasoning patterns,
	to use OWL and OWL reasoners instead.

# Reference
- <http://www.uio.no/studier/emner/matnat/ifi/INF3580/v16/undervisningsmateriale/>