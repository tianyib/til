# Update one item of a ListView when any propety of this item changed

The first thing is binding the data source of this ListView with an [ObservableCollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.observablecollection-1?view=netcore-3.1), cause it can notify ListView of any changes.

Then, you can use any of these following methods:

- ## Implement ListView item as INotifyPropertyChanged

Inherit the view model of ListView items from [BindableObject](https://docs.microsoft.com/en-us/dotnet/api/Xamarin.Forms.BindableObject?view=xamarin-forms) and call [OnPropertyChanged](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.bindableobject.onpropertychanged?view=xamarin-forms) after properties were changed.

- ## Set value to it's self after ListView item was changed
```c#
listItems[listItems.IndexOf(item)] = item;
```
If ListView item does not implement [IEquable](https://docs.microsoft.com/en-us/dotnet/api/system.iequatable-1?view=netcore-3.1), use foreach to locate changed item.
```c#
foreach (var item in listItems)
  if (item.Id == changedItemId)
    item = item;
```
