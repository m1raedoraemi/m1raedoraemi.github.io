---
title: Semantic Technologies 2
date: 2018-04-01 15:19:45
tags:
- RDF
---

# Semantic Technologies 2
# Lecture 3 는 Skip (Jena)
# Lecture 4
## SPARQL
SPARQL Protocol And RDF Query Language

### People called “Martin Giese”
```sql
Select ?who Where{
	?who foaf:Name "Martin Giese" .
}
```

### Publications by people called “Martin Giese”
```sql
Select ?pub Where{
	?who foaf:Name "Martin Giese" .
	?pub dc:creator ?who .
}
```

### Titles of publications by people called “Martin Giese”
```sql
Select ?title Where{
	?who foaf:Name "Martin Giese" .
	?pub dc:creator ?who .
	?pub dc:title ?title .
}
```

### Names of people who have published with “Martin Giese”
```sql
Select DISTINCT ?name Where{
	?who foaf:Name "Martin Giese" .
	?pub dc:creator ?who .
	?pub dc:creator ?other .
	?other foaf:Name ?name .
}
```

## Group Graph Patterns
A group containing two groups:
```sql
{
	{ _:pub1 dc:creator ?mg . }
	{ _:pub2 dc:creator ?other . }
}
```

## Filters
Numerical functions, string operations, reg. exp. matching, etc.

```sql
{
	?x a dbpedia-owl:Place ;
		dbpprop:population ?pop .
	FILTER (?pop > 1000000)
}
```

```sql
{
	?x a dbpedia-owl:Place ;
		dbpprop:abstract ?abs .
	FILTER (lang(?abs) = "no")
}
```

## Optional Patterns
A match can leave some variables unbound.

```sql
{
	?x a dbpedia-owl:Place ;
		dbpprop:population ?pop .
	OPTIONAL {
		?x dbpprop:abstract ?abs .
		FILTER (lang(?abs) = "no")
	}
}
```

## Matching Alternatives :UNION
합집합
```sql
{
	{ ?book dc:creator ?author ;
			dc:created ?date . }
	UNION
	{ ?book foaf:maker ?author . }
	UNION
	{ ?author foaf:made ?book . }
}
```

## Four Types of Queries
- SELECT Compute table of bindings for variables
- CONSTRUCT Use bindings to construct a new RDF graph
- ASK Answer (yes/no) whether there is ≥ 1 match
- DESCRIBE Answer available information about matching resources

## Solution Modifiers
Sequence modifiers can modify the solution sequence:
- Order
- Projection
- Distinct
- Reduce
- Offset
- Limit

### Distinct
DISTINCT eliminates duplicate solutions:
### Reduced
흠.. ?
REDUCE allows to remove some or all duplicate solutions

# Reference
- <http://www.uio.no/studier/emner/matnat/ifi/INF3580/v16/undervisningsmateriale/>