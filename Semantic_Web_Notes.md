### the Definition of Deep web & Dark web
![](http://www.learnenglishwithwill.com/wp-content/uploads/2017/09/dark-net-dark-web-deep-net.jpg)
### the Structure of Semantic Web
**Metadata + Ontologies =Linked Data (Web of Data)**

### RDF data model 
info available as tables in relational db and csv files

#### 1. literals
literal is data encoded as a string;
literal value can have a XML language tag;
literal         a datatype
visualized as a rectangle in graph
#### 2. resources
Global identifiers: 
URL(Locator): specialization of URI via hTTP
URI(Identifier): it doesn't need to call back anything (ftp,http,https..)
URN(Name):  specialization of URI, only specifies its name(no info back in browser)
IRI: unicode char set
**Relationship Graph**
IRI/URI syntax: query ? fragment #
URI schemes: http,https, ftp,urn,oid...
Semantic Web advocates HTTP URI/IRIs
Blank Node: node with no name, automatically generate name from sys(name depends on particular sys)   
arise from embedded descriptions   
#### 3. Statement(triples)
property between two resources  
#### 4. graphs
RDF graph = set of triples  
#### 5. datasets and quads
Adding the graph into a triple can be important!  

### RDF Syntax: 
Serialization: represent graph as liner text
Alternative serialization for diff needs: 
1. for human read
**N-triples**:
IRIs are enclosed in <>
syntax: sub1 predicate1 obj1
**Turtle**: extend N3 easier to read  
TriG: extend Turtle for representing datasets
N-quads: 
2. for machines
RDF/XML
3. For web programming
JSON-LD for Javascript and Python
4. Embedding in web pages: 
RDFa(embed RDF in HTML pages) **Facebook is using it now**

### RDF Schema
object-oriented way to represent it.
classes and instances
class and prop hierachy
properties and constraints
