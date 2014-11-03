
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

- alternatives: how to handle alternative parts:
 * ex : left palm/right palm

Tooling:
========
- a small tool could be provided to help add bom entries (rather trivial)
