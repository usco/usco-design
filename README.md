Experimental wrappers around "designs" /things/physibles /Etc


Thoughts on data structures: 

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
