# Convert switch statement to expression
Beginning with C# 8.0, you use the switch expression to evaluate a single expression from a list of candidate expressions based on a pattern match with an input expression.
### statement:
```c#

switch (condition)
{
  case 1:
    result = value1 + value2;
    break;
  case 2:
    result = value1 - value2;
    break;
  default:
    result = 0;
    break;
}
```
### expression:
```c#
result = condition switch
{
  1 => value1 + value2,
  2 => value1 - value2,
  _ => 0,
};
```
