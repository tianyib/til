# Convert switch statement to expression
## statement:
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
## expression:
```c#
result = condition switch
{
  1 => value1 + value2,
  2 => value1 - value2,
  _ => 0,
};
```
