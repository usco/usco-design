Experimental wrappers around "designs" /things/physibles /Etc
and thoughts about design configuration files (bom, assemblies, build instructrions etc)


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
- (parametric, reuse etc)

user friendly
=============

if bom, assembly etc files are missing ask the user if he/she
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

  state (string): state of the design (concept,???)
  description (text/html): description of the design
  
  thumbnail-urls:[
    primary_image_id (int): reference to the primary image of the design
  ],
  authors:[
   {
    name:text
    url: text
   }
  ],
  licenses:[
   (string): license of the design (cc, ccnc or gplv3)
  ]
  tags: ["youmagine", "superduperdesign"],
  
  created_at (timestamp): timestamp when the design was created
  updated_at (timestamp): timestamp when the design was last updated
  
  //
  annotations: either link to file or json here
  bom: either link to file or json here
  assemblies: either link to file or json here
  

}
