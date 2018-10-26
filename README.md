# CSV (Inline) Meta Data Formats


[CSV in CSV](#csv-in-csv) •
[Attribute-Relation "Classic"](#attribute-relation-classic) •
[Attribute-Relation "Inline"](#attribute-relation-inline) •
[Front Matter in YAML](#front-matter-in-yaml) •


## CSV in CSV

Use CSV meta data in CSV :-). How? 

The CSV in CSV Meta Data Block Rule No 1.:  If the first record / line
starts with `Col,Name` or `Name,Type` than it's a meta data block
until the next blank line.


Example:

```
##########################
# try with some comments
#   and blank lines even header

Col, Name
1,   Brewery
2,   City
3,   Name
4,   Abv


Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```

Note: You can add optional fields as you like to the meta data block.




## Attribute-Relation "Classic"

Use the ARFF (attribute-relation file format)-like alternative style
with `%` for comments and `@`-directives
for "meta data" in the header (before any records):

```
%%%%%%%%%%%%%%%%%%
% try with some comments
%   and blank lines even before @-directives in header

@RELATION Beer

@ATTRIBUTE Brewery
@ATTRIBUTE City
@ATTRIBUTE Name
@ATTRIBUTE Abv

@DATA
Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```


## Attribute-Relation "Inline"

Use the ARFF (attribute-relation file format)-like alternative style with  `@`-directives
inside comments (for easier backwards compatibility with old readers)
for "meta data" in the header (before any records):

```
##########################
# try with some comments
#   and blank lines even before @-directives in header
#
# @RELATION Beer
#
# @ATTRIBUTE Brewery
# @ATTRIBUTE City
# @ATTRIBUTE Name
# @ATTRIBUTE Abv

Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```

## Front Matter in YAML

Use a front matter meta data block in YAML.
The front matter must start with `---` before the first record (in the header)
and ends with `---`.

```
##########################
# try with some comments
#   and blank lines even before front matter block

---
fields:
- name: Brewery
- name: City
- name: Name
- name: Abv
---

Andechser Klosterbrauerei,Andechs,Doppelbock Dunkel,7%
Augustiner Bräu München,München,Edelstoff,5.6%

Bayerische Staatsbrauerei Weihenstephan,  Freising,  Hefe Weissbier,   5.4%
Brauerei Spezial,                         Bamberg,   Rauchbier Märzen, 5.1%
Hacker-Pschorr Bräu,                      München,   Münchner Dunkel,  5.0%
Staatliches Hofbräuhaus München,          München,   Hofbräu Oktoberfestbier, 6.3%
```



## Examples


### `tree-ops.csv` in Metadata Vocabulary for Tabular Data by W3C

Let's use the example from
[Metadata Vocabulary for Tabular Data](https://www.w3.org/TR/tabular-metadata/)
by the World Wide Web Consortium (W3C)
and compare CSV meta data formats.


`tree-ops.csv`:

```
GID,On Street,Species,Trim Cycle,Inventory Date
1,ADDISON AV,Celtis australis,Large Tree Routine Prune,10/18/2010
2,EMERSON ST,Liquidambar styraciflua,Large Tree Routine Prune,6/2/2010
```

and the meta data recommended (proposed) by the W3C:

`tree-ops.csv-metadata.json`:

``` json
{
  "@context": ["http://www.w3.org/ns/csvw", {"@language": "en"}],
  "url": "tree-ops.csv",
  "dc:title": "Tree Operations",
  "dcat:keyword": ["tree", "street", "maintenance"],
  "dc:publisher": {
    "schema:name": "Example Municipality",
    "schema:url": {"@id": "http://example.org"}
  },
  "dc:license": {"@id": "http://opendefinition.org/licenses/cc-by/"},
  "dc:modified": {"@value": "2010-12-31", "@type": "xsd:date"},
  "tableSchema": {
    "columns": [{
      "name": "GID",
      "titles": ["GID", "Generic Identifier"],
      "dc:description": "An identifier for the operation on a tree.",
      "datatype": "string",
      "required": true
    }, {
      "name": "on_street",
      "titles": "On Street",
      "dc:description": "The street that the tree is on.",
      "datatype": "string"
    }, {
      "name": "species",
      "titles": "Species",
      "dc:description": "The species of the tree.",
      "datatype": "string"
    }, {
      "name": "trim_cycle",
      "titles": "Trim Cycle",
      "dc:description": "The operation performed on the tree.",
      "datatype": "string"
    }, {
      "name": "inventory_date",
      "titles": "Inventory Date",
      "dc:description": "The date of the operation that was performed.",
      "datatype": {"base": "date", "format": "M/d/yyyy"}
    }],
    "primaryKey": "GID",
    "aboutUrl": "#gid-{GID}"
  }
}
```

That's obviously not for humans but for machines.


Let's start with a CSV in CSV meta data version:


```
######################################
# title:     Tree Operations
# keyword:   tree, street, maintenance
# publisher: Example Municipality
# license:   CC BY
# update:    2010-12-31

Name,            Type,    Required,  Primary, Format,   Titles,                   Description
GID,             string,  true,      true,            , GID | Generic Identifier, An identifier for the operation on a tree.  
on_street,       string,      ,          ,            , On Street,                The street that the tree is on.       
species,         string,      ,          ,            , Species,                  The species of the tree.
trim_cycle,      string,      ,          ,            , Trim Cycle,               The operation performed on the tree. 
inventory_date,  date,        ,          ,    M/d/yyyy, Inventory Date,           The date of the operation that was performed.


GID, On Street,  Species,                 Trim Cycle,               Inventory Date
1,   ADDISON AV, Celtis australis,        Large Tree Routine Prune, 10/18/2010
2,   EMERSON ST, Liquidambar styraciflua, Large Tree Routine Prune, 6/2/2010
```


Or lets use two meta data blocks (for easier reading):

```
######################################
# title:     Tree Operations
# keyword:   tree, street, maintenance
# publisher: Example Municipality
# license:   CC BY
# update:    2010-12-31

Name,            Type,    Required,  Primary, Format   
GID,             string,  true,      true              
on_street,       string                    
species,         string            
trim_cycle,      string
inventory_date,  date,    ,          , M/d/yyyy

Name,            Titles,                   Description
GID,             GID | Generic Identifier, An identifier for the operation on a tree. 
on_street,       On Street,                The street that the tree is on.
species,         Species,                  The species of the tree.
trim_cycle,      Trim Cycle,               The operation performed on the tree. 
inventory_date,  Inventory Date,           The date of the operation that was performed.

GID, On Street,  Species,                 Trim Cycle,               Inventory Date
1,   ADDISON AV, Celtis australis,        Large Tree Routine Prune, 10/18/2010
2,   EMERSON ST, Liquidambar styraciflua, Large Tree Routine Prune, 6/2/2010
```

Voila! It's starting to get readable.


Or how about a version with front matter in YAML:

```
---
######################################
# title:     Tree Operations
# keyword:   tree, street, maintenance
# publisher: Example Municipality
# license:   CC BY
# update:    2010-12-31

fields:
- name:     GID
  type:     string
  required: true     
  primary:  true            
  titles:   [GID, Generic Identifier]
  description: An identifier for the operation on a tree.  

- name:     on_street
  type:     string
  titles:   [On Street]
  description: The street that the tree is on.       

- name:     species
  type:     string
  titles:   [Species]                  
  description: The species of the tree.

- name:      trim_cycle
  type:      string      
  titles:    [Trim Cycle]
  description: The operation performed on the tree. 

- name:      inventory_date
  type:      date
  format:    M/d/yyyy
  titles:    [Inventory Date]
  description:  The date of the operation that was performed.
---

GID, On Street,  Species,                 Trim Cycle,               Inventory Date
1,   ADDISON AV, Celtis australis,        Large Tree Routine Prune, 10/18/2010
2,   EMERSON ST, Liquidambar styraciflua, Large Tree Routine Prune, 6/2/2010
```










## License

The CSV Meta formats are dedicated to the public domain.



## Request for Comments (RFC)

Please post your comments to the [wwwmake forum](http://groups.google.com/group/wwwmake).
Thanks!

