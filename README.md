# CSV (Inline) Meta Data Formats





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




## ARFF "Classic"

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


## ARFF "Inline"

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



## License

The CSV Meta formats are dedicated to the public domain.



## Request for Comments (RFC)

Please post your comments to the [wwwmake forum](http://groups.google.com/group/wwwmake).
Thanks!

