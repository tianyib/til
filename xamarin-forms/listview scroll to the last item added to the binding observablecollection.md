## ListView scroll to the last item added to the binding ObservableCollection in MVVM way
ViewModel.cs after collection changed add:
```c#
MessagingCenter.Send<object, object> (this, "ListViewItemAdded", lastItem);
```
where lastItem is last item in the collection.

Page.xaml.cs add:
```c#
MessagingCenter.Unsubscribe<object, object>(this, "ListViewItemAdded");
MessagingCenter.Subscribe<object, object> (this, "ListViewItemAdded", (sender, arg) => {
    MainScreenMessagesListView.ScrollTo(arg, ScrollToPosition.End, true);
});
```
