## Binding Entry to nullable int
It'll probably occur a null convertion error, if you binding an Entry to a int property. How to fix it?

- #### Create a value converter.
```c#
class NullableIntConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var result = string.Empty();
        
        if (value is int intValue)
        {
            result = intValue.ToString();
        }
        
        return resutl;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        int result = 0;

        if (int.TryParse(stringValue, out intValue))
        {
            result = intValue;
        }

        return result;
    }
}
```
and use it in your page
```c#
<Entry Text="{Binding Number, Mode=TwoWay, Converter={StaticResource NullableIntConverter}}" Placeholder="Number" Keyboard="Numeric" />
```
- #### Binding to string properties and adding conversion in the accessors.
in ViewModel:
```c#
protected decimal _price = 0;
public decimal Price
{
    get => _price;
    set => SetProperty(ref _price, value, nameof(Price), () => OnPropertyChanged(nameof(StrPrice)));
}
public string StrPrice
{
    get => _price.ToString();
    set
    {
        Price = int.TryParse(value, out int result) ? result : 0;
    }
}
```
in BaseViewModel:
``` c#
protected bool SetProperty<T>(ref T backingStore, T value, [CallerMemberName]string propertyName = "",
    Action onChanged = null, Action onChanging = null)
{
    if (EqualityComparer<T>.Default.Equals(backingStore, value))
        return false;

    onChanging?.Invoke();

    backingStore = value;

    onChanged?.Invoke();
    OnPropertyChanged(propertyName);
    return true;
}
```
in Page:
```c#
<Entry Text="{Binding StrPrice, Mode=TwoWay}" Placeholder="Number" Keyboard="Numeric" />
```
