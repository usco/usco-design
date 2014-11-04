
Notes about Assemblies:
=======================
- they are acyclic graphs: 
  *  they specify hierarchies of objects (parent -> children) 
- they reference parts by ids from bom : assemblies do not contain direct
references to meshes/parts, but always reference the part from the bom !
- they specify relative positions, rotations and scaling 
- they can also be used to created exploded views :
 * leaf nodes in the hierarchy are "exploded" first 
 * then up the hierarchy

- they could also be used for assembly instructions (they specify the position and 
orientation of parts after they are assembled)
- sensible defaults: the position , rotation and scale of parts should only be specified
if they differ from the defaults (position: [0,0,0], rotation [0,0,0] and scale [1,1,1])
this saves on file complexity, size and bandswidth and makes things clearer
 

Questions:
----------

- one assembly or multiple ones ?
 * if multiple ones how to specify the main one (the fully assembled design/project)
- alternative assemblies : 
  * if there are multiple possibles assemblies for a final design, how can it be handled
- parametric assemblies ?
 * perhaps parametric designs can generate their own assembly datastructure on the fly?
- connectors: should connectors be specified at the assembly level or elsewhere
- also, should joints be specified in assemblies ?


