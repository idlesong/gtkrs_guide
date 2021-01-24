## Tutorial Tree, List and Icon Grid Widgets
![alt text](./images/list-and-tree.png) ![alt text](./images/list-box.png)

- Tree and List Widget Overview — Overview of GtkTreeModel, GtkTreeView, and friends
- [TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel.html) — The tree interface used by GtkTreeView
- [TreeSelection](https://gtk-rs.org/docs/gtk/struct.TreeSelection.html) — The selection object for GtkTreeView
- [TreeViewColumn](https://gtk-rs.org/docs/gtk/struct.TreeViewColumn.html) — A visible column in a GtkTreeView widget
- [TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView.html) — A widget for displaying both trees and lists
- [TreeView drag-and-drop](https://gtk-rs.org/docs/gtk/struct.FlowBox.html) — Interfaces for drag-and-drop support in GtkTreeView
- [CellView](https://gtk-rs.org/docs/gtk/struct.CellView.html) — A widget displaying a single row of a GtkTreeModel
- [IconView](https://gtk-rs.org/docs/gtk/struct.IconView.html) — A widget which displays a list of icons in a grid
- [TreeSortable](https://gtk-rs.org/docs/gtk/struct.TreeSortable.html) — The interface for sortable models used by GtkTreeView
- [TreeModelSort](https://gtk-rs.org/docs/gtk/struct.TreeModelSort.html) — A GtkTreeModel which makes an underlying tree model sortable
- [TreeModelFilter](https://gtk-rs.org/docs/gtk/struct.TreeModelFilter.html) — A GtkTreeModel which hides parts of an underlying tree model
- [CellLayout](https://gtk-rs.org/docs/gtk/struct.CellLayout.html) — An interface for packing cells
- [CellArea](https://gtk-rs.org/docs/gtk/struct.CellArea.html) — An abstract class for laying out GtkCellRenderers
- [CellAreaBox](https://gtk-rs.org/docs/gtk/struct.CellAreaBox.html) — A cell area that renders GtkCellRenderers into a row or a column
- [CellAreaContext](https://gtk-rs.org/docs/gtk/struct.CellAreaContext.html) — Stores geometrical information for a series of rows in a GtkCellArea
- [CellRenderer](https://gtk-rs.org/docs/gtk/struct.CellRenderer.html) — An object for rendering a single cell
- [CellEditable](https://gtk-rs.org/docs/gtk/struct.CellEditable.html) — Interface for widgets that can be used for editing cells
- [CellRendererAccel](https://gtk-rs.org/docs/gtk/struct.CellRendererAccel.html) — Renders a keyboard accelerator in a cell
- [CellRendererCombo](https://gtk-rs.org/docs/gtk/struct.CellRendererCombo.html) — Renders a combobox in a cell
- [CellRendererPixbuf](https://gtk-rs.org/docs/gtk/struct.CellRendererPixbuf.html) — Renders a pixbuf in a cell
- [CellRendererProgress](https://gtk-rs.org/docs/gtk/struct.RendererProgress.html) — Renders numbers as progress bars
- [CellRendererSpin](https://gtk-rs.org/docs/gtk/struct.RendererSpin.html) — Renders a spin button in a cell
- [CellRendererText](https://gtk-rs.org/docs/gtk/struct.RendererText.html) — Renders text in a cell
- [CellRendererToggle](https://gtk-rs.org/docs/gtk/struct.RendererToggle.html) — Renders a toggle button in a cell
- [CellRendererSpinner](https://gtk-rs.org/docs/gtk/struct.RendererSpinner.html) — Renders a spinning animation in a cell
- [ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore.html) — A list-like data structure that can be used with the GtkTreeView
- [TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore.html) — A tree-like data structure that can be used with the GtkTreeView

examples [simple_treeview](simple_treeview.rs),[treeview](treeview.rs),[list_store](listbox_model.rs), [tree_model_sort](tree_model_sort.rs)

## Tree and List Widgets

A [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) and its associated widgets are an extremely powerful way of displaying data. They are used in conjunction with a [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) or [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) and provide a way of displaying and manipulating data in many ways, including:
- Automatic updates when data is added, removed or edited
- Drag and drop support
- Sorting data
- Embedding widgets such as check boxes, progress bars, etc.
- Reorderable and resizable columns
- Filtering data

With the power and flexibility of a [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) comes complexity. It is often difficult for beginner developers to be able to utilize it correctly due to the number of methods which are required.

## The Model

Each [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) has an associated [gtk::TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel), which contains the data displayed by the TreeView. Each [gtk::TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel) can be used by more than one [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView). For instance, this allows the same underlying data to be displayed and edited in 2 different ways at the same time. Or the 2 Views might display different columns from the same Model data, in the same way that 2 SQL queries (or “views”) might show different fields from the same database table.

Although you can theoretically implement your own Model, you will normally ue either the [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) or [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) model classes. [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) contains simple rows of data, and each row has no children, whereas [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) contains rows of data, and each row may have child rows.

When constructing a model you have to specify the data types for each column the model holds.
```store = gtk::ListStore(str, str, float)```

This creates a list store with three columns, two string columns, and a float column.

Adding data to the model is done using `gtk::ListStore.append()` or `gtk::TreeStore.append()`, depending upon which sort of model was created.

For a [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore):
``` rust
treeiter = store.append(["The Art of Computer Programming",
                         "Donald E. Knuth", 25.46]);
```

For a [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) you must specify an existing row to append the new row to, using a [gtk::TreeIter](https://gtk-rs.org/docs/gtk/struct.TreeIter), or None for the top level of the tree:

``` rust
treeiter = store.append(None, ["The Art of Computer Programming",
                               "Donald E. Knuth", 25.46]);
```

Both methods return a [gtk::TreeIter](https://gtk-rs.org/docs/gtk/struct.TreeIter) instance, which points to the location of the newly inserted row. You can retrieve a [gtk::TreeIter](https://gtk-rs.org/docs/gtk/struct.TreeIter) by calling gtk::TreeModel.get_iter().

Once data has been inserted, you can retrieve or modify data using the tree iter and column index.

```
println!(store[treeiter][2]); // Prints value of third column
store[treeiter][2] = 42.15;
```

As with Python’s built-in list object you can use len() to get the number of rows and use slices to retrieve or set values.

``` rust
// Print number of rows
println!(len(store));
// Print all but first column
println!(store[treeiter][1:]);
// Print last column
println!(store[treeiter][-1]);
// Set last two columns
store[treeiter][1:] = ["Donald Ervin Knuth", 41.99];
```

Iterating over all rows of a tree model is very simple as well.
``` rust
for row in store {
  // Print values of all columns
  println(row[:]);
}
```

Keep in mind, that if you use [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore), the above code will only iterate over the rows of the top level, but not the children of the nodes. To iterate over all rows, use `gtk::TreeModel.foreach()`.
``` rust
fn print_row(store, treepath, treeiter){
  println!("\t" * (treepath.get_depth() - 1), store[treeiter][:], sep="");
}
store.foreach(print_row);
```

Apart from accessing values stored in a [gtk::TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel) with the list-like method mentioned above, it is also possible to either use [gtk::TreeIter](https://gtk-rs.org/docs/gtk/struct.TreeIter) or [gtk::TreePath](https://gtk-rs.org/docs/gtk/struct.TreePath) instances. Both reference a particular row in a tree model. One can convert a path to an iterator by calling `gtk::TreeModel.get_iter()`. As [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) contains only one level, i.e. nodes do not have any child nodes, a path is essentially the index of the row you want to access.

``` rust
// Get path pointing to 6th row in list store
path = gtk::TreePath(5);
treeiter = liststore.get_iter(path);
// Get value at 2nd column
value = liststore.get_value(treeiter, 1);
```

In the case of [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore), a path is a list of indexes or a string. The string form is a list of numbers separated by a colon. Each number refers to the offset at that level. Thus, the path “0” refers to the root node and the path “2:4” refers to the fifth child of the third node.

``` rust
// Get path pointing to 5th child of 3rd row in tree store
path = gtk::TreePath([2, 4]);
treeiter = treestore.get_iter(path);
 // Get value at 2nd column
value = treestore.get_value(treeiter, 1);
```

Instances of [gtk::TreePath](https://gtk-rs.org/docs/gtk/struct.TreePath) can be accessed like lists, i.e. len(treepath) returns the depth of the item treepath is pointing to, and treepath[i] returns the child’s index on the i-th level.

## The View

While there are several different models to choose from, there is only one view widget to deal with. It works with either the list or the tree store. Setting up a [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) is not a difficult matter. It needs a [gtk::TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel) to know where to retrieve its data from, either by passing it to the [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) constructor, or by calling [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView).set_model().

``` rust
let tree_view = TreeView::new();
let tree_store = TreeStore::new(&[String::static_type()]);

tree_view.set_model(Some(&tree_store));
```

Once the [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) widget has a model, it will need to know how to display the model. It does this with columns and cell renderers.

Cell renderers are used to draw the data in the tree model in a way. There are a number of cell renderers that come with GTK+, for instance [gtk::CellRendererText](https://gtk-rs.org/docs/gtk/struct.CellRendererText), [gtk::CellRendererPixbuf](https://gtk-rs.org/docs/gtk/struct.CellRendererPixbuf) and [gtk::CellRendererToggle](https://gtk-rs.org/docs/gtk/struct.CellRendererToggle). In addition, it is relatively easy to write a custom renderer yourself.

A [gtk::TreeViewColumn](https://gtk-rs.org/docs/gtk/struct.TreeViewColumn) is the object that [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) uses to organize the vertical columns in the tree view. It needs to know the name of the column to label for the user, what type of cell renderer to use, and which piece of data to retrieve from the model for a given row.

To render more than one model column in a view column, you need to create a [gtk::TreeViewColumn](https://gtk-rs.org/docs/gtk/struct.TreeViewColumn) instance and use `gtk::TreeViewColumn.pack_start()` to add the model columns to it.

``` rust
let column = TreeViewColumn::new();
let cell = CellRendererText::new();

column.pack_start(&cell, true);
column.add_attribute(&cell, "text", 0);
tree.append_column(&column);
```

## The Selection

Most applications will need to not only deal with displaying data, but also receiving input events from users. To do this, simply get a reference to a selection object and connect to the “changed” signal.

``` rust
select = tree.get_selection()
select.connect("changed", on_tree_selection_changed)

/// rust code
let selection = tree.get_selection();
selection.connect_changed(clone!(@weak right_tree => move |tree_selection| {
}
```

Then to retrieve data for the row selected:
``` rust
def on_tree_selection_changed(selection):
    model, treeiter = selection.get_selected()
    if treeiter is not None:
        println!("You selected", model[treeiter][0])

/// rust code
let selection = tree.get_selection();
selection.connect_changed(clone!(@weak right_tree => move |tree_selection| {
  let (left_model, iter) = tree_selection.get_selected().expect("Couldn't get selected");        
}
```

#### Example: treeview.rs
``` rust
//! # TreeView Sample
//!
//! This sample demonstrates how to create a TreeView with a ListStore.

extern crate gio;
extern crate gtk;

use gio::prelude::*;
use gtk::prelude::*;
use gtk::{
    ApplicationWindow, CellRendererText, Label, ListStore, Orientation, TreeView, TreeViewColumn,
    WindowPosition,
};

use std::env::args;

fn create_and_fill_model() -> ListStore {
    // Creation of a model with two rows.
    let model = ListStore::new(&[u32::static_type(), String::static_type()]);

    // Filling up the tree view.
    let entries = &["Michel", "Sara", "Liam", "Zelda", "Neo", "Octopus master"];
    for (i, entry) in entries.iter().enumerate() {
        model.insert_with_values(None, &[0, 1], &[&(i as u32 + 1), &entry]);
    }
    model
}

fn append_column(tree: &TreeView, id: i32) {
    let column = TreeViewColumn::new();
    let cell = CellRendererText::new();

    column.pack_start(&cell, true);
    // Association of the view's column with the model's `id` column.
    column.add_attribute(&cell, "text", id);
    tree.append_column(&column);
}

fn create_and_setup_view() -> TreeView {
    // Creating the tree view.
    let tree = TreeView::new();

    tree.set_headers_visible(false);
    // Creating the two columns inside the view.
    append_column(&tree, 0);
    append_column(&tree, 1);
    tree
}

fn build_ui(application: &gtk::Application) {
    let window = ApplicationWindow::new(application);

    window.set_title("Simple TreeView example");
    window.set_position(WindowPosition::Center);

    // Creating a vertical layout to place both tree view and label in the window.
    let vertical_layout = gtk::Box::new(Orientation::Vertical, 0);

    // Creation of the label.
    let label = Label::new(None);

    let tree = create_and_setup_view();

    let model = create_and_fill_model();
    // Setting the model into the view.
    tree.set_model(Some(&model));
    // Adding the view to the layout.
    vertical_layout.add(&tree);
    // Same goes for the label.
    vertical_layout.add(&label);

    // The closure responds to selection changes by connection to "::cursor-changed" signal,
    // that gets emitted when the cursor moves (focus changes).
    tree.connect_cursor_changed(move |tree_view| {
        let selection = tree_view.get_selection();
        if let Some((model, iter)) = selection.get_selected() {
            // Now getting back the values from the row corresponding to the
            // iterator `iter`.
            //
            // The `get_value` method do the conversion between the gtk type and Rust.
            label.set_text(&format!(
                "Hello '{}' from row {}",
                model
                    .get_value(&iter, 1)
                    .get::<String>()
                    .expect("Treeview selection, column 1")
                    .expect("Treeview selection, column 1: mandatory value not found"),
                model
                    .get_value(&iter, 0)
                    .get_some::<u32>()
                    .expect("Treeview selection, column 0"),
            ));
        }
    });

    // Adding the layout to the window.
    window.add(&vertical_layout);

    window.show_all();
}

fn main() {
    let application = gtk::Application::new(
        Some("com.github.gtk-rs.examples.simple_treeview"),
        Default::default(),
    )
    .expect("Initialization failed...");

    application.connect_activate(|app| {
        build_ui(app);
    });

    application.run(&args().collect::<Vec<_>>());
}

```

You can control what selections are allowed by calling `gtk::TreeSelection.set_mode()`. `gtk::TreeSelection.get_selected()` does not work if the selection mode is set to `gtk::SelectionMode.MULTIPLE`, use `gtk::TreeSelection.get_selected_rows()` instead.

## Sorting

Sorting is an important feature for tree views and is supported by the standard tree models ([gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) and [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore)), which implement the gtk::TreeSortable interface.
13.4.1. Sorting by clicking on columns

A column of a [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) can easily made sortable with a call to `gtk::TreeViewColumn.set_sort_column_id()`. Afterwards the column can be sorted by clicking on its header.

First we need a simple [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) and a [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) as a model.
```
model = gtk::ListStore(str)
model.append(["Benjamin"])
model.append(["Charles"])
model.append(["alfred"])
model.append(["Alfred"])
model.append(["David"])
model.append(["charles"])
model.append(["david"])
model.append(["benjamin"])

treeView = gtk::TreeView(model=model)

cellRenderer = gtk::CellRendererText()
column = gtk::TreeViewColumn("Title", renderer, text=0)
```
The next step is to enable sorting. Note that the column_id (0 in the example) refers to the column of the model and not to the TreeView’s column.

```column.set_sort_column_id(0)```

#### Setting a custom sort function

It is also possible to set a custom comparison function in order to change the sorting behaviour. As an example we will create a comparison function that sorts case-sensitive. In the example above the sorted list looked like:
```
alfred
Alfred
benjamin
Benjamin
charles
Charles
david
David
```

The case-sensitive sorted list will look like:
```
Alfred
Benjamin
Charles
David
alfred
benjamin
charles
david
```
First of all a comparison function is needed. This function gets two rows and has to return a negative integer if the first one should come before the second one, zero if they are equal and a positive integer if the second one should come before the second one.
```
def compare(model, row1, row2, user_data):
    sort_column, _ = model.get_sort_column_id()
    value1 = model.get_value(row1, sort_column)
    value2 = model.get_value(row2, sort_column)
    if value1 < value2:
        return -1
    elif value1 == value2:
        return 0
    else:
        return 1
```
Then the sort function has to be set by

```gtk::TreeSortable.set_sort_func().```

```model.set_sort_func(0, compare, None)```

## Filtering

Unlike sorting, filtering is not handled by the two models we previously saw, but by the gtk::TreeModelFilter class. This class, like [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) and gtk::ListStore, is a [gtk::TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel). It acts as a layer between the “real” model (a [gtk::TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore) or a [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore)), hiding some elements to the view. In practice, it supplies the [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) with a subset of the underlying model. Instances of gtk::TreeModelFilter can be stacked one onto another, to use multiple filters on the same model (in the same way you’d use “AND” clauses in a SQL request). They can also be chained with gtk::TreeModelSort instances.

You can create a new instance of a gtk::TreeModelFilter and give it a model to filter, but the easiest way is to spawn it directly from the filtered model, using the `gtk::TreeModel.filter_new()` method.

```filter = model.filter_new()```

In the same way the sorting function works, the gtk::TreeModelFilter uses a “visibility” function, which, given a row from the underlying model, will return a boolean indicating if this row should be filtered out or not. It’s set by ```gtk::TreeModelFilter.set_visible_func():```

```filter.set_visible_func(filter_func, data=None)```

The alternative to a “visibility” function is to use a boolean column in the model to specify which rows to filter. Choose which column with gtk::TreeModelFilter.set_visible_column().

Let’s look at a full example which uses the whole [gtk::ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore) - ```gtk::TreeModelFilter``` - ```gtk::TreeModelFilter``` - [gtk::TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView) stack.
