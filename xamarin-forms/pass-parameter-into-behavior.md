## Pass Parameter into Behavior

Samply add a public property to the Behavior.

Example as follows.

In your behavior:

``` c#
public class MaxLengthEntry : Behavior<Entry>
{
    public int MaxLength { get; set; } = int.MaxValue;

    protected override void OnAttachedTo(Entry bindable)
    {
        base.OnAttachedTo(bindable);
        bindable.TextChanged += OnEntryTextChanged;
    }

    protected override void OnDetachingFrom(Entry bindable)
    {
        bindable.TextChanged -= OnEntryTextChanged;
        base.OnDetachingFrom(bindable);
    }

    void OnEntryTextChanged(object sender, TextChangedEventArgs e)
    {
        if (e.NewTextValue.Length > MaxLength)
        {
            ((Entry)sender).Text = e.NewTextValue.Substring(0, MaxLength);
        }
    }
}
```
In your xaml:
``` c#
<Entry>
  <Entry.Behaviors>
    <behaviors:MaxLengthEntry MaxLength="8"/>
  </Entry.Behaviors>
</Entry>
```
