
Notes about BOM:
================
- printed parts need to be included in the dom : (how else would one know how many
of each to print ?)

- titles/name should be singular in 99% of cases : they are title for a single unit

- versioning : a bom entry for versionable parts should always contain a version number
 * version number SHOULD use semantic versioning (minor, major, patch)

- amounts vs lengths vs weight etc :
  * both are needed: they describe different things: the size of each "stuff"
  * even better: lengths, weights should describe atomic stuff

- local vs global ids:
 * both are needed : local ids to reference things within the local context
 * global ids are needed to have trully unique ids

- a bom entry can either describe an "end product" (leaf) like a 3d printed mesh, a nut,
a bolt etc,  or a composite (another composite etc), see 
https://github.com/garyhodgson/thing-tracker-network/wiki/Ideas-for-BOMs,-Sub-assemblies-and-Parts

- alternatives: how to handle alternative parts ?
 * ex : left palm/right palm

- parameters for parametric designs:
  * how to handle pre-generated stls from parametric designs vs the parametric designs with 
a given set of params ?
  * parts which use the same parametric design #with different parameters# need different 

- gcode/machine presets:
  * this should be optional
  * this is metadata, a very specific , should be treated as such
  * ideally , they should be specified in the bom entry for a specific part : different
  contexts == different printing/gcode settings 

- parts libraries: extremely important , see parts librairies section in this document

- the thing-tracker spec already has a lot of these things and is adaptable: DO NOT reinvent
the wheel
 * ttn is allready adopted 
 * spec can still be updated at this stage
 * lots of sane design decisions
 * "Bolts" librairy will be available through it: see below
 * https://github.com/garyhodgson/thing-tracker-network/wiki/Conventions-and-Guidelines 


Part librairies:
================
- ideally a bom should contain references to data about all sorts of parts, some printed
some not
- a lot of parts are standard based and somewhat immutable (bolts, nuts), the BOLTS
librairy http://www.bolts-library.org/en/index.html already has most of the data, models, 
and "bindings" (openscad, freecad etc) that are needed


Example data structure:
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
           "implementations": {
              "src/hand.scad":"assets/thumb_x_x_x.stl",
              "src/hand.freecad":"assets/thumb_x_x_x_free.stl"
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
         
         


Tooling:
========
- a small tool could be provided to help add bom entries (rather trivial)
