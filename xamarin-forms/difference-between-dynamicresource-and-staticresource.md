# Defference between DynamicResource and StaticResource

The `DynamicResource` markup extension is similar to the `StaticResource` markup extension in that both use a dictionary key to fetch a value from a `ResourceDictionary`. 

- ## StaticResource
The `StaticResource` performs ***a single dictionary lookup***. 
It will only be assigned once and any changes to resource dictionary during runtime will be ignored.

- ## DynamicResource 
The `DynamicResource` ***maintains a link*** to the dictionary key. 
Therefore, if the dictionary entry associated with the key is replaced, the change is applied to the visual element.
