---
title: Semantic Technologies 1
date: 2018-04-01 15:19:45
tags:
- RDF
---

# Semantic Technologies
# Lecture 1
## For Standards
[RDF, OWL, SPARQL, etc. ](http://www.w3.org/2001/sw/wiki/Main_Page)

## Bringing it together
### RDF as common knowledge format:
movie:StarWars7 movie:director people:jj.
people:jj people:name "J. J. Abrams".
### URIs to avoid naming conflicts:
http://heim.ifi.uio.no/martingi/movies#StarWars7
### existing protocols to move data:
Use HTTP for queries to a semantic web server
Use XML for answers, to encode RDF, etc.
### OWL to express ontologies
### Reasoners to infer new knowledge

## The AAA Slogan
Anyone can say Anything 
- good, simple ,necessary
- difficult to trust data
- difficult to to locate relevant information
- have to deal with enormous amounts of data

## Semantic technologies
### Let’s have a look at what we have
- W3C standards: RDF, SPARQL, OWL, some more
- Technology like reasoners, ontology editors
- Interfacing to relational databases, etc.

## Data integration
![](Semantic%20Technologies/AB1D7A50-7E9D-4E04-8B99-6353D687773B.png)

![](Semantic%20Technologies/6778918C-E986-4455-A9E6-E79F2F83EFA6.png)

# Exercise 1
[Java Project Link](http://media.wiley.com/product_ancillary/1X/04704180/DOWNLOAD/Code%20Package%20with%20Jars%20--%20Chapter%2001-04.zip)

# Lecture 2
## RDF : W3C Overview
- The Resource Description Framework (RDF) is a standard model for data interchange on the Web.
- It extends the linking structure of the Web to use URIs to name the relationship between things as well as the two ends of the link.
- This linking structure forms a directed, labelled graph.

## RDF Triples
- All information in RDF is expressed using a triple pattern.
-  A triple consists of a subject, a predicate, and an object.
- Examples:
	- subject + predicate + object
	- Norway + has capital + Oslo
-  Another word for an RDF triple is a ~statement or fact.~
- The elements of an RDF triple are either (URI references, blank nodes, or literals)

## Uniform Resource Identifiers (URIs)
- RDF (Resource Description Framework) talks about resources.
- Resources are identified by URIs (Uniform Resource Identifiers).
	- Norway: http://dbpedia.org/resource/Norway
	- has capital: http://dbpedia.org/ontology/capital
	- Oslo: http://dbpedia.org/resource/Oslo

## URIs and QNames
- URIs are often long and hard to read and write.
- Most serialisations use an abbreviation mechanism.
	- Define ~“prefixes”, “namespaces”.~
	- RDF/XML format: XML namespaces and entities.
- E.g., in Turtle serialisation:
@prefix dbp: <http://dbpedia.org/resource/> .
- A QName like dbp:Oslo stands for http://dbpedia.org/resource/Oslo
- Remember: ~It’s all just URIs!~

## Literals
- Literals are used to represent data values.
- All literals have a datatype.
- Datatypes are also resources, referenced via URIs, and written as:
	- dbp:Oslo dbp-ont:population "629313"^^xsd:integer .
- However, if nothing is written, it is assumed to be a string:
	- dbp:Oslo dbp-ont:officialName "Oslo" .
	- dbp:Oslo dbp-ont:officialName "Oslo"^^xsd:string .
- One can also specify the language of a string using a language tag:
dbp:Norway rdfs:label "Norge"@no 

## RDF Graph
- An RDF graph is a set of triples. E.g.,
	- dbp:Norway dbp-ont:capital dbp:Oslo .
	- dbp:Oslo dbp-ont:population "629313"^^xsd:integer .

![](Semantic%20Technologies/2C32D0C6-E00B-477B-AE21-13F217A75714.png)

## Blank nodes
- Blank nodes are like resources without a URI.
- Use when resource is unknown, or has no (natural) identifier.

![](Semantic%20Technologies/8DE682E2-9606-4731-9492-52AFA368DE86.png)

## Triple Grammer

![](Semantic%20Technologies/8B8BFB05-AEAA-445F-B700-BFEAE279BE73.png)

- - - -
## Vocabularies : RDF, RDFS
- RDF: describing RDF graphs.
rdf:Statement

rdf:subject
rdf:predicate
rdf:object

rdf:type
- RDFS: describing RDF vocabularies.
rdfs:Class

rdfs:subClassOf,
rdfs:subPropertyOf

rdfs:domain,
rdfs:range

rdfs:label

- Examples:
	- dbp:Oslo rdf:type dbp-ont:Place .
	- dbp:Norway rdfs:label "Norge"@no .
	- dbp:Capital rdfs:subClassOf dbp:City .

- - - -

## RDF Serialisations
There are many serialisations for the RDF data model:
- RDF/XML the W3C standard. Complicated!
- Turtle convenient, human readable/writable—our choice.
- N-triples one triple per line. No abbreviations
- N3, TriX, TriG, RDF/JSON, . . .

## Turtle
### Full URIs are surrounded by < and >:
`<http://dbpedia.org/resource/Oslo>`
### Statements are triples terminated by a period:
`<http://dbpedia.org/resource/Oslo> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://dbpedia.org/ontology/Place> .`
### Use ‘a’ to abbreviate rdf:type:
`<http://dbpedia.org/resource/Oslo> a <http://dbpedia.org/ontology/Place> .`

### Namespace prefixes are declared with @prefix:
`@prefix dbp: <http://dbpedia.org/resource/> .`

### Literal values are enclosed in double quotes:
`dbp:Oslo :officialName "Oslo" .`
### Possibly with type or language information:
```
dbp:Norway rdfs:label "Norge"@no .
dbp:Oslo :population "629313"^^xsd:integer .
```
### Numbers and booleans may be written without quotes:
```
dbp:Oslo :population 629313 .
dbp:Oslo :isCapital true .
```
### . . . statements may share a subject with ‘;’:
__Before__
```
dbp:Oslo :officialName "Oslo" .
dbp:Oslo :population 629313 .
dbp:Oslo :leaderName dbp:Fabian_Stang .
```

__After__
```
dbp:Oslo 	:officialName "Oslo" ;
			:population 629313 ;
			:leaderName dbp:Fabian_Stang .
```

### . . . and in combination:
```
dbp:Norway rdfs:label "Norway"@en, "Norwegen"@de, "Norge"@no ;
			:capital dbp:Oslo .
```


# Reference
- <http://www.uio.no/studier/emner/matnat/ifi/INF3580/v16/undervisningsmateriale/>