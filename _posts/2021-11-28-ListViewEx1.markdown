---
layout: post
title:  "WinUI3 ListView with an Empty state - the issue"
permalink: listviewex1
date:   2021-11-29 00:00:00 +0000

---
One of the things I like about the `CollectionView` in Xamarin.Forms is that it has built-in support for showing specific, different content when the collection is empty. This is important for a UX perspective as it's important to clearly distinguish between when a list is empty because there is no content to show or when it's empty for another reason. The WinUI3 `ListView` doesn't have this capability so I'm writing this post as the start of a series exploring how to improve and extend the ListView control, starting with adding a way to show specific UI when the list is empty.

Let's start by looking at issue I want to try and address.

At a simplistic level, the XAML file may contain something like this.

```xml
<Grid>
    <ListView
        ItemsSource="{x:Bind AvailableItems}"
        ItemTemplate="{StaticResource AvailableItemTemplate}" />
    <TextBlock
        Visibility="{x:Bind ShowNoItemsMessage}"
        Text="No items available"
        VerticalAlignment="Center"
        HorizontalAlignment="Center"
        HorizontalTextAlignment="Center" />
</Grid>
```

There are three controls here:

- The `ListView` that actually shows the items.
- A `TextBlock` to show a message when the list is empty.
- A `Grid` to make it easy to group the above two items together.

This is where we start to see the problems:

- We've got three controls where we'd like to only have one. Having only one control would make the XAML simpler and it would make the purpose of the content of the XAML file clearer.

There's also another big problem.

- The logic for the displaying of the message is contained in the DataContext (ViewModel) that we're binding to. This means the logic for whether to display a UI message is contained inside the ViewModel.

We're mixing logic for the application and the logic for displaying a data related state. It's easy to argue that this display logic is specific to the application but it's very generic and something that will often be repeated multiple times in most applications. It would be beneficial to only have to write this logic once and reuse it everywhere.

There are ways of addressing these issues and my intention is to explore them in following posts...
