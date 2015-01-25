Experimental wrappers around "designs" /things/physibles /Etc
and thoughts about design configuration files (bom, assemblies, build instructrions etc)


put simply:
===========
usco-design is a wrapper around :
 - n number of files: stl, amf, scad etc
 - configuration files
 - is also representing a git repo (or similar)
 
 should:
 - support versioning
 - forking
 
how to handle parametric designs:
=================================

Questions:
----------
- have a "main" entry like in node's package.json files that points to 
the main script ?
- for custom element wrapping , how do we expose attributes ?
 * the user either creates them manually
 * or selects what parameters to take (generation of custom element)
 * somehow parse parameters from the scad/jscad/coscad files ?
 * attribute names alone : 
   - are they good enough ? do we brute force regeneration of 
 the design if any of them changes ?
   - experimental "future version"  has partial regeneration but this can not
   be used for all cases
 
See more thougts about custom elements below


Packaging a design as custom element
------------------------------------
Advantages:
 - dynamic (change an attribute, design is regenerated)
 - using proxy pattern, can be used both for client side & server side generation
 - easy to create UI for
 

configuration files
===================
- similar to a package manager's json files in a lot of ways (see npm , bower etc)
- ability to specify dependencie (other parts and/or designs)
- ability to specify specific versions of other designs
- should be agnostic to the internal formats (stl, amf, obj, etc) up to a point....
- everything in one configuration file vs multiple ones? perhaps both should
be allowed (by simply have a url to other json files)


bom is essential
================

- bom entry leafs are either parts , raw materials etc
- boms allow for composites : each bom entry can also be a composite

Questions
---------
- boms should also have version numbers for parts?

Notes
-----
- boms are NOT assemblies: boms list the amount of each item,
give parts numbers, but they do not contain positioning data etc 
- for parametric parts it is ESSENTIAL to specify the used parameters
- boms are used by a lot of other systems : 
 * assemblies (structure of parts in relation to each other)
 * build instructions (what steps are needed to build this or that composite)
 

notion of "features" of parts
-------------------- --------
- (parametric, reuse etc) : a feature is a "governing" attribute:  it is bad practice
to expose too many parameters if a single one can be used to account for the various 
possible variations


user friendly
=============

In the end, it is just a set of files, a wrapper ui(s?) to make it accessible
to end users should be relatively easy to do

Questions:
---------
- if bom, assembly etc files are missing ask the user if he/she
wants to add them ?


more technical
==============
- redundant hierarchy of packages like npm ...
- or flat like bower ?


Thoughts on data structures: 
============================


Design:
{
  id (int): id of the design : uuid 
  name (string): name of the design
  description (text/html): description of the design
  version : (string) : a semantic versioning based design version
  url: (string) root location for a design
  
  authors:[
   {
    name:text
    url: text
   }
  ],
  licenses:[
   (string): license of the design (cc, ccnc or gplv3 etc)
  ]
  tags: ["youmagine", "superduperdesign"], : list of strings
  
  thumbnail-urls:[
    primary_image_id (int): reference to the primary image of the design
  ],
  
  
  created_at (timestamp): timestamp when the design was created
  updated_at (timestamp): timestamp when the design was last updated
  
  meta:{
    state (string): state of the design (concept,???)
  }
  
  //
  annotations: either link to file or json here
  bom: either link to file or json here
  assemblies: either link to file or json here

}


update jan 19 th 2015
=====================

- a "design" is pretty much like a (bower/npm) package
- a "design should be forkable"

- semantic versioning and purely visual/static design : perhaps ANY change could be considered
a breaking api change ? what is an api in the case of  a visual design ? 
perhaps simply "if you can replace 'as is' the old part with the new, without any additional
changed, then it is not a breaking change ?


- essential fields to find a good design : 
  * users evaluation/ rating (levels are better than just likes ?)
  * last update date (to prune/reject stale designs)
  * forks
  * author (s) (tendency to favor "miracle workers" ? )
  

RANDOM IDEAS
------------

- auto semantic versioner: use git diffs etc to keep track of changes to functions 
etc (changed api) to detect breaking/ non breaking changes
   * auto update version number accordingly etc etc

