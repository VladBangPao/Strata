# GobbledyGook

Gobbledy gook is the subset of schema that is sufficiently generalizable to the extent that we can apply the same methods to it and always be doing something orderly, predictable, and useful with Gobbledy Gook utilities.

## Schema Pattern Algorithm

#### What about schema?
1. what is a good description of any given schema?
      - That depends on whether we are key pattern agnostic

      - If we are agnostic, we are searching for a pattern on the permutation of the set \[ '[', '{' \]
            - Once we have a pattern, what do we do with it as an intermediate step?

      - If we are not key agnostic, we are searching first for key patterns, then checking to see if they follow a recurring pattern on the set \[ '[', '{' \] from top to bottom, where the base case is everything following the termination of the pattern
            - Once we have a pattern, what do we do with it as an intermediate step? 

2. based on that description is it well formed and consistent?
      - what we mean by well formed is that recursion from the top level is of a single type. What we mean by consistent is that recursion has a very consistent recursion to base case level ratio across multiple paths from the root of sufficient depth.
3. If it is well formed and consistent, what is the best way to use it?
      - If it is not consistent but is well formed what is the best way to use it?
      - If it is not well formed but is consistent, what is the best way to use it?
4. How do we test a good description? 
      - My opinion is that the way we generate tests is the way the schema is described.
      We are still answering these questions

### Postulation
1. There is some theoretical limit on the number of permutations that are possible in the set \[ '[', '{' \] that are possible before recurrence in a key agnostic setting. If we are not key agnostic, then this postulation does not matter
2. We need a recursive path validation step before we return the all of the recursive schema steps for a given path

### Axioms
1. '[' and '{' are the recognized set of generalizable recursive containers that can have any arbitrary number of keys or elements (at any level) without us needing to treat the algorithm below with any less generality than is stated.
2. For every recursive pattern there is an objective min and max number of levels to a recursive case that is agnostic to key names
3. When we are not key agnostic, we wish to find the minimum number of levels for any recursive case
4. When we are key agnostic, we wish to find the maximum number of levels for any recursive case (this guarantees recursion is valid at the least)
5. We treat each recursive path seperately from the top level, because some schema can be recursively used in multiple ways so long as they have different roots


## General Base Algorithm 
(this is not particularly useful without answering the questions above, but it is sufficiently general to build upon)
      
        gobbledy(gook){
          if(gook){
              if(Array.isArray(gook)){
                  for(var i = 0; i<gook.length; i++){
                      this.gobbledy(gook[i])
                  }
              }else if(typeof gook === 'object'){
                  var keys = Object.keys(gook)
                  if(keys.length){
                    for(var i = 0; i<keys.length; i++){
                        this.gobbledy(gook[keys[i]])
                    }
                  }
              }
          }
          return
      }
      
## Recursive Walk     

      
                                                                                                           B
                                                                                                           |                                       
                                                                                                           |
                                                                                                           v
      [                                                                                                    ]   
          {                   a:                  },  {                    a:                          }    
              [                                  ]      [                                         ]         
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:  }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}                



      _________________________________________________________________________________________________________
                                                                                                            
                                                                                                       B                                           
                                                                                                       |    
                                                                                                       |    
      [                                                                                                v   ]   
          {                   a:                  },  {                    a:                          }    
              [                                  ]      [                                         ]         
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:  }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}                




      _____________________________________________________________________________________________________
                                                                                                             
                                                                           B                                                                       
                                                                           |                                
                                                                           |                                
      [                                                                    v                               ]   
          {                   a:                  },  {                    a:                          }    
              [                                  ]      [                                         ]         
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:  }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}                


      ______________________________________________________________________________________________________


      [                                                                                      B             ]
          {                   a:                  },  {                    a:                |         }
              [                                  ]      [                                    v     ]
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:   }
                    [   ]       [   ]                           [     ]         [   ]  [   ]
                      {}          {}                             1, {}            {}     {}





      _____________________________________________________________________________________________________
      
      [                                                                                  B                ]
          {                   a:                  },  {                    a:            |            }
              [                                  ]      [                                v        ]
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             




      _____________________________________________________________________________________________________
      
      [                                                                                                   ]
          {                   a:                  },  {                    a:                         }
              [                                  ]      [                                 B       ]
                  {   a:  },  {   b:  }                        {   a:  },    {   a:,    b:|  }             
                    [   ]       [   ]                           [     ]         [   ]  [  v]                  
                      {}          {}                             1, {}            {}     {}             





     _______________________________


     [                                                                                   B                 ]
          {                   a:                 },  {                    a:             |             }
              [                              ]          [                                v         ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      _______________________________
      
      [                                                                                       B              ]
          {                   a:                 },  {                    a:                  |        }
              [                              ]          [                                     v    ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      _____________________________________________________________________________________________________

      [                                                                           B                          ]
          {                   a:                 },  {                    a:      |                    }
              [                              ]          [                         v               ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      ________________________________________________________________________________________________________
      
      [                                                                                                      ]
          {                   a:                 },  {                    a:     B                     }
              [                              ]          [                        |                ]
                  {   a:  },  {   b:  }                       {    a:   },    {  |a:,    b:   }             
                    [   ]       [   ]                           [     ]         [v  ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             





      ________________________________

      [                                                                           B                         ]
          {                   a:                 },  {                    a:      |                   }
              [                              ]          [                         v               ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      _________________________________

      [                                                                                       B            ]
          {                   a:                 },  {                    a:                  |       }
              [                              ]          [                                     v   ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             




      
      _________________________________
      
                                                                                                  B
      [                                                                                           |        ]
          {                   a:                 },  {                    a:                      v   }
              [                              ]          [                                         ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



 

      ________________________________________________________________________________________________________


      [                                                       B                                            ]
          {                   a:                 },  {        |           a:                          }
              [                              ]          [     v                                   ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             




      ______________________________________________________________________________________________________        


      [                                                            B                                       ]
          {                   a:                 },  {             |      a:                          }
              [                              ]          [          v                              ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      _______________________________________________________________________________________________________

      [                                                                                                    ]
          {                   a:                 },  {                    a:                          }
              [                              ]          [            B                            ]
                  {   a:  },  {   b:  }                       {    a:|  },    {   a:,    b:   }             
                    [   ]       [   ]                           [    v]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             


  

      _________________________________

      [                                                            B                                       ]
          {                   a:                 },  {             |       a:                          }
              [                              ]          [          v                              ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             



      
      
      _______________________________________________________________________________________________________

      [                                                                                                    ]
          {                   a:                 },  {                     a:                          }
              [                              ]          [        B                                ]
                  {   a:  },  {   b:  }                       {  | a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [v    ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             




      ________________________________

      [                                                            B                                       ]
          {                   a:                 },  {             |       a:                          }
              [                              ]          [          v                              ]
                  {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                    [   ]       [   ]                           [     ]         [   ]  [   ]                  
                      {}          {}                             1, {}            {}     {}             


     

      _________________________________
                                                                                                      B
      [                                                                                               |        ]
            {                   a:                 },   {                     a:                      v   }
                  [                              ]          [                                         ]
                      {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                        [   ]       [   ]                           [     ]         [   ]  [   ]                  
                          {}          {}                             1, {}            {}     {}             



      _________________________________
                                                                                                          B
                                                                                                          |
      [                                                                                                   v    ]
            {                   a:                 },   {                     a:                          }
                  [                              ]          [                                         ]
                      {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                        [   ]       [   ]                           [     ]         [   ]  [   ]                  
                          {}          {}                             1, {}            {}     {}             



      _________________________________
                                                                                                              B 
                                                                                                              |
                                                                                                              v
      [                                                                                                       ]
            {                   a:                 },   {                     a:                          }
                  [                              ]          [                                         ]
                      {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                        [   ]       [   ]                           [     ]         [   ]  [   ]                  
                          {}          {}                             1, {}            {}     {}             




      _______________________________________________________________________________________________________

                                                   B 
                                                   |
                                                   |
      [                                            v                                                           ]
            {                   a:                 },   {                     a:                          }
                  [                              ]          [                                         ]
                      {   a:  },  {   b:  }                       {    a:   },    {   a:,    b:   }             
                        [   ]       [   ]                           [     ]         [   ]  [   ]                  
                          {}          {}                             1, {}            {}     {}             





      etc....

