# Update one item of a ListView when any propety of this item changed

The first thing is binding the data source of this ListView with an ObservableCollection, cause it can notify ListView of any changes.

Then, you can use any of these following methods:

- ## Implement ListView item as INotifyPropertyChanged

Inherit the view model of ListView items from BindableObject and call OnPropertyChanged after properties were changed.

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
