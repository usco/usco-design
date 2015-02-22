
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
- any partId with an id higher than the last item in the bom is an
 "assembled/composite part " ?
 
 
Possible source of reuse/inspirations
-------------------------------------

- urdf file http://wiki.ros.org/urdf & similar formats 
  Interesting points: 
  - it is not a scene graph per se, but a more flat descriptive format
  https://github.com/ros/urdf_tutorial/blob/master/urdf/05-visual.urdf
  - parent child relationships are described **as joints of various types**, which could be
  VERY usefull for E-nable like & small robotics projects etc , the available joint types are:
  
      * revolute - a hinge joint that rotates along the axis and has a limited range specified by the upper and lower limits.
      * continuous - a continuous hinge joint that rotates around the axis and has no upper and lower limits
      * prismatic - a sliding joint that slides along the axis, and has a limited range specified by the upper and lower limits.
      * fixed - This is not really a joint because it cannot move. All degrees of freedom are locked. This type of joint does not require the axis, calibration, dynamics, limits or safety_controller.
      * floating - This joint allows motion for all 6 degrees of freedom.
      * planar - This joint allows motion in a plane perpendicular to the axis.
  
  


