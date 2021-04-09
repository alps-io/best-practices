# best-practices
A repo where we share/explore best/common/recommended practices when using ALPS 

## State

A semantic descriptor that is a web page contains other semantic descriptors, and they are linked to each other. Such a page semantic descriptor is represented by an upper camel case.

```json
  "id": "BlogPosting", "type": "semantic", "def": "https://schema.org/BlogPosting",
  "descriptor": [
    {"href": "#id"}, 
    {"href": "#articleBody"}, 
    {"href": "#dateCreated"},
    {"href": "#blog"}
  ]
```

## Safe state transition

A simple `safe` request is represented by appending a `go` prefix to the descriptor of the next transition destination.

```
  {"id": "goHome", "type": "safe", "rt": "#Home"},
  {"id": "goFirst", "type": "safe", "rt": "#TodoList"},
  {"id": "goPrevious", "type": "safe", "rt": "#TodoList"},
```

@mamund -- I also use "doCreate" and "doUpdate" for unsafe and idempotent actions"

## ALPS file structure

The description of the ALPS descriptor is divided into the following three blocks, which are represented in the following order.

1. semantic descriptors for word definitions with `def` or `doc` (ontology)
2. semantic descriptor group for inclusion relations (taxonomy)
3. semantic descriptors for state transitions (choreography)

```json
descriptor" : [
    {"id" : "name", "type" : "semantic", "def": "http://schema.org/identifier"},
    {"id" : "age", "type" : "semantic", "def": "http://schema.org/title"},

    {"id" : "Person", "type": "semantic", "descriptor":
        [
          {"href": "#name"},
          {"href": "#age"}
        ]
    }
    
    {"id": "goPerson", "type": "safe", "rt": "#Person"},
]
```

## Hierarchical structures outside ALPS

ALPS can represent hierarchical meanings by position.

```json
"descriptor": [
    {"id": "name", "def": "https://schema.org/name"},
    {"id": "product", "descriptor":[{"href": "#name"}]}
    {"id": "person", "descriptor":[{"href": "#name"}]}
]
```

In the above example, `name` is shared with `product/name` and `person/name`.
The basic rule is to follow the practices of each format when representing such words in a format with only a flat hierarchy.

* In the html case, it is represented by the Lower camel case.

```
<form>
    <input name="productName" type="text">
    <input name="personName" type="text">
</form>
```
