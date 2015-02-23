
Notes about BOM:
================
- printed parts need to be included in the dom : (how else would one know how many
of each to print ?)

- flat vs tree: flat is better, what are the use cases for a tree ? 

- titles/name should be singular in 99% of cases : they are title for a single unit
  HOWEVER :
    **both are needed** : title is the human readeable string , while name is meant as
    machine useable (but somewhat human readable)

- versioning : a bom entry for **versionable parts** should always contain a version number
 * version number SHOULD use semantic versioning (minor, major, patch)

- amounts vs lengths vs weight etc :
  * ie how do you describe "15 pieces of string of 15cm each"
  * both are needed: they describe different things: the size of each "stuff"
  * (not sure about this) even better: lengths, weights should describe atomic stuff
  
    > **SPEC v1:**
    > 
    > - **amount** for ... amounts 
    > - **size** for the distances, weight etc
  	>


- local vs global ids:
 * both are needed : local ids to reference things within the local context
 * global ids are needed to have trully unique ids
  
  	> **SPEC v1:**
    > - global ids (uuids) are now called **uid** in the bom
  	>

- a bom entry can either describe an "end product" (leaf) like a 3d printed mesh, a nut,
a bolt etc,  or a composite (another composite etc), see 
https://github.com/garyhodgson/thing-tracker-network/wiki/Ideas-for-BOMs,-Sub-assemblies-and-Parts

- alternatives: how to handle alternative parts ?
 * ex : left palm/right palm
 * ??????

- parameters for parametric designs:
  * how to handle pre-generated stls from parametric designs vs the parametric designs with 
a given set of params ?
  * parts which use the same parametric design #with different parameters# need different 
  
  > **SPEC v1:**
  >  - **parameters** field can be added per bom entry
  >


- gcode/machine presets:
  * this should be optional
  * this is metadata, a very specific , should be treated as such
  * ideally , they should be specified in the bom entry for a specific part : different
  contexts == different printing/gcode settings 

- parts libraries: extremely important , see parts librairies section in this document

	> **NOTES** 
    > 
    > the Thing-Tracker-Network spec already has a lot of these things and is adaptable: DO NOT reinvent the wheel (if possible)
 	> * spec can still be updated at this stage
	> * lots of sane design decisions
    > * "Bolts" library will be available through it: see below
    > * https://github.com/garyhodgson/thing-tracker-network/wiki/Conventions-and-Guidelines 


Part librairies:
================
- ideally a bom should contain references to data about all sorts of parts, some printed
some not
- a lot of parts are standard based and somewhat immutable (bolts, nuts), the BOLTS
librairy http://www.bolts-library.org/en/index.html already has most of the data, models, 
and "bindings" (openscad, freecad etc) that are needed



Referencing external parts??
============================
- closely related to "part librairies" above
- simple url is sufficient to point to another design ?

- **important** : a BOM might have overlaps with the design.json dependencies field,
but a BOM only describes "concrete" things: ie
  * even if your parametric design for PART-A makes use of 2 different other designs, (all referenced as dependencies in the dependencies fields), it does not mean they show up in the BOM !
  
  simple example : 
   * you are creating an enclosure for a raspberry-pi
   * somebody provides a design package for a fully modelled raspi called "raspi"
   * your design.json might look like (simplified)
   
   
   	  {
        	"name":"raspi-cool-case",
            "title":"raspi cool case",
            "description":"bla bla",
  		  "version": "0.0.1",
            "dependencies":{
               "https://youmagine.com/designer/raspi":"0.1.0",
               "https://youmagine.com/designer/BOLTS":"0.2.3"
            }
         }

  * while your bom might look like this:
    

     {
           "id":0,
           "title":"Case bottom",
           "name": "case-bottom",
           "version":"0.0.1",
           "description":"The enclosure's bottom",
           "amount": 1,
           "unit":"EA",
           "implementations": 
            {"cad/case.scad":"cad/case-bottom-0.0.1.stl"},
           "parameters":"{type:'bottom'}"
      },
         
      {
           "id":1,
           "title":"Case top",
           "name": "case-top",
           "version":"0.0.1",
           "description":"The enclosure's top",
           "amount": 1,
           "unit":"EA",
           "implementations": {
              "cad/case.scad":"cad/case-top-0.0.1.stl",
            },
           "parameters":"{type:'top',gpio:false}"
       },

As you can see, the **raspi** design/package does not show up at all in the bom since it was very likely used only in the Openscad file to generate the enclosure.

To make it clearer : ** a BOM only ever contains actual/ physical/ real objects that you used to build your design**


Example data structures:
=======================

      {
         "id":15,
         "title":"Palm",
         "version":"2.2.0",
         "description":"Right Palm",
         "amount": 1,
         "unit":"EA",
         "url":"palm.scad",
         "parameters":"{orientation:'Right',innerSize:25}",
         
      }

  Possible data structure for pre-generated stl from a parametric design
  -----------------------------------------------------------------------
  
          {
           "id":15,
           "title":"Palm",
           "version":"2.2.0",
           "description":"Right Palm",
           "amount": 1,
           "unit":"EA",
           "implementations": 
            {"hand.scad":"palm_x_x_x.stl"},
           "parameters":"{type:'palm',orientation:'Right',innerSize:25}"
         },
         
            {
           "id":16,
           "title":"Thumb",
           "version":"2.2.0",
           "description":"Thumb",
           "amount": 2,
           "unit":"EA",
           "url": "bla.com/designs/thumb"
           "implementations": {
              "src/hand.scad":"assets/thumb_2.2.0_scad.stl",
              "src/hand.freecad":"assets/thumb_2.2.0_freecad.stl"
            },
           "parameters":"{type:'thumb',orientation:'Right',innerSize:25}"
         },
         
          {
           "id":17,
           "title":"Thumb",
           "version":"2.2.0",
           "description":"Thumb",
           "amount": 2,
           "unit":"EA",
           "implementations": {
            "default":"bla.stl"}
         },
         //reference other design, not local ?
          {
           "id":18,
           "title":"Special",
           "version":"0.2.0",
           "description":"Some special stuff",
           "amount": 1,
           "unit":"EA",
           "implementations": {
            "default":"https://foobar.com/designs/special"}
         },
         
         


Tooling:
========
- a small tool could be provided to help add bom entries 
