# Defference between DynamicResource and StaticResource

The DynamicResource markup extension is similar to the StaticResource markup extension in that both use a dictionary key to fetch a value from a ResourceDictionary. 

## StaticResource
The StaticResource performs <b>a single dictionary lookup</b>. 
It will only be assigned once and any changes to resource dictionary during runtime will be ignored.

## DynamicResource
The DynamicResource <b>maintains a link</b> to the dictionary key. 
Therefore, if the dictionary entry associated with the key is replaced, the change is applied to the visual element.
