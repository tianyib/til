# switch expression
The ```switch``` expression provides for ```switch```-like semantics in an expression context. It provides a concise syntax when the switch arms produce a value. 
### example 1
The following example shows the structure of a switch expression. It translates values from an ```enum``` representing visual directions in an online map to the corresponding cardinal direction:
```c#
public static class SwitchExample
{
    public enum Directions
    {
        Up,
        Down,
        Right,
        Left
    }

    public enum Orientation
    {
        North,
        South,
        East,
        West
    }

    public static void Main()
    {
        var direction = Directions.Right;
        Console.WriteLine($"Map view direction is {direction}");

        var orientation = direction switch
        {
            Directions.Up    => Orientation.North,
            Directions.Right => Orientation.East,
            Directions.Down  => Orientation.South,
            Directions.Left  => Orientation.West,
        };
        Console.WriteLine($"Cardinal orientation is {orientation}");
    }
}
```
### example 2
Many patterns are supported in switch expression arms. The preceding example used a value pattern. 
```c#
public static T TypeExample<T>(IEnumerable<T> sequence) =>
    sequence switch
    {
        System.Array array => (T)array.GetValue(2),
        IList<T> list      => list[2],
        IEnumerable<T> seq => seq.Skip(2).First(),
    };
```
### example 3
Patterns can be recursive, where a pattern tests a type, and if that type matches, the pattern matches one or more property values on the range expression. You can use recursive patterns to extend the preceding example. 
```c#
public static T RecursiveExample<T>(IEnumerable<T> sequence) =>
    sequence switch
    {
        System.Array { Length : 0}       => default(T),
        System.Array { Length : 1} array => (T)array.GetValue(0),
        System.Array { Length : 2} array => (T)array.GetValue(1),
        System.Array array               => (T)array.GetValue(2),
        IList<T> list                    => list[2],
        IEnumerable<T> seq               => seq.Skip(2).First(),
    };
```
### example 4
Recursive patterns can examine properties of the range expression, but can't execute arbitrary code. You can use a case guard, specified in a when clause, to provide similar checks for other sequence types:
```c#
public static T CaseGuardExample<T>(IEnumerable<T> sequence) =>
    sequence switch
    {
        System.Array { Length : 0}                => default(T),
        System.Array { Length : 1} array          => (T)array.GetValue(0),
        System.Array { Length : 2} array          => (T)array.GetValue(1),
        System.Array array                        => (T)array.GetValue(2),
        IEnumerable<T> list when !list.Any()      => default(T),
        IEnumerable<T> list when list.Count() < 3 => list.Last(),
        IList<T> list                             => list[2],
        IEnumerable<T> seq                        => seq.Skip(2).First(),
    };
```
### example 5
Finally, you can add the ```_``` pattern and the ```null``` pattern to catch arguments that aren't processed by any other switch expression arm. That makes the switch expression exhaustive, meaning any possible value of the range expression is handled. The following example adds those expression arms:
```c#
public static T ExhaustiveExample<T>(IEnumerable<T> sequence) =>
    sequence switch
    {
        System.Array { Length : 0}       => default(T),
        System.Array { Length : 1} array => (T)array.GetValue(0),
        System.Array { Length : 2} array => (T)array.GetValue(1),
        System.Array array               => (T)array.GetValue(2),
        IEnumerable<T> list
            when !list.Any()             => default(T),
        IEnumerable<T> list
            when list.Count() < 3        => list.Last(),
        IList<T> list                    => list[2],
        null                             => throw new ArgumentNullException(nameof(sequence)),
        _                                => sequence.Skip(2).First(),
    };
```
The preceding example adds a ```null``` pattern, and changes the ```IEnumerable<T>``` type pattern to a ```_``` pattern. The null pattern provides a ```null``` check as a switch expression arm. The expression for that arm throws an [`ArgumentNullException`](https://docs.microsoft.com/en-us/dotnet/api/system.argumentnullexception). The ```_``` pattern matches all inputs that haven't been matched by previous arms. It must come after the null check, or it would match ```null``` inputs.
