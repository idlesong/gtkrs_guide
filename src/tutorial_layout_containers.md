## Layout Containers
widgets | description
---|---
- | [GtkBox](https://gtk-rs.org/docs/gtk/struct.Box.html) — A container for packing widgets in a single row or column
![alt text](./images/grid-packing.png) | [GtkGrid](https://gtk-rs.org/docs/gtk/struct.Grid.html) — Pack widgets in rows and columns
![alt text](./images/list-box.png) | [GtkListBox](https://gtk-rs.org/docs/gtk/struct.ListBox.html) — A list container
- | [GtkFlowBox](https://gtk-rs.org/docs/gtk/struct.FlowBox.html) — A container that allows reflowing its children
![alt text](./images/notebook.png) | [GtkNotebook](https://gtk-rs.org/docs/gtk/struct.Notebook.html) — A tabbed notebook container
- | [GtkOverlay](https://gtk-rs.org/docs/gtk/struct.Overlay.html) — A container which overlays widgets on top of each other [demo]
![alt text](./images/headerbar.png) | [GtkHeaderBar](https://gtk-rs.org/docs/gtk/struct.HeaderBar.html) — A box with a centered child
![alt text](./images/panes.png) | [GtkPaned](https://gtk-rs.org/docs/gtk/struct.Paned.html) — A widget with two adjustable panes
- | More full list
![alt text](./images/stack.png) | [GtkStack](https://gtk-rs.org/docs/gtk/struct.Stack.html) — A stacking container
![alt text](./images/stackswitcher.png) | [GtkStackSwitcher](https://gtk-rs.org/docs/gtk/struct.StackSwitcher.html) — A controller for GtkStack
- | [GtkStackSidebar](https://gtk-rs.org/docs/gtk/struct.StackSidebar.html) — An automatic sidebar widget
- | [GtkRevealer](https://gtk-rs.org/docs/gtk/struct.Revealer.html) — Hide and show with animation
- | [GtkActionBar](https://gtk-rs.org/docs/gtk/struct.ActionBar.html) — A full width bar for presenting contextual actions
- | [GtkButtonBox](https://gtk-rs.org/docs/gtk/struct.ButtonBox.html) — A container for arranging buttons
- | [GtkLayout](https://gtk-rs.org/docs/gtk/struct.Layout.html) — Infinite scrollable area containing child widgets and/or custom drawing
- | [GtkExpander](https://gtk-rs.org/docs/gtk/struct.Expander.html) — A container which can hide its child
- | [GtkOrientable](https://gtk-rs.org/docs/gtk/struct.Orientable.html) — An interface for flippable widgets
- | [GtkAspectFrame](https://gtk-rs.org/docs/gtk/struct.AspectFrame.html) — A frame that constrains its child to a particular aspect ratio
- | [GtkFixed](https://gtk-rs.org/docs/gtk/struct.Fixed.html) — A container which allows you to position widgets at fixed coordinates

[grid.rs](grid.rs) [listbox](listbox.rs) [notebook](notebook.rs)

While many GUI toolkits require you to precisely place widgets in a window, using absolute positioning, GTK+ uses a different approach. Rather than specifying the position and size of each widget in the window, you can arrange your widgets in rows, columns, and/or tables. The size of your window can be determined automatically, based on the sizes of the widgets it contains. And the sizes of the widgets are, in turn, determined by the amount of text they contain, or the minimum and maximum sizes that you specify, and/or how you have requested that the available space should be shared between sets of widgets. You can perfect your layout by specifying padding distance and centering values for each of your widgets. GTK+ then uses all this information to resize and reposition everything sensibly and smoothly when the user manipulates the window.

GTK+ arranges widgets hierarchically, using containers. They are invisible to the end user and are inserted into a window, or placed within each other to layout components. There are two flavours of containers: single-child containers, which are all descendants of Gtk.Bin, and multiple-child containers, which are descendants of Gtk.Container. The most commonly used are vertical or horizontal boxes (Gtk.Box) and grids (Gtk.Grid).

### Boxes

Boxes are invisible containers into which we can pack our widgets. When packing widgets into a horizontal box, the objects are inserted horizontally from left to right or right to left depending on whether Gtk.Box.pack_start() or Gtk.Box.pack_end() is used. In a vertical box, widgets are packed from top to bottom or vice versa. You may use any combination of boxes inside or beside other boxes to create the desired effect.

1.Example
Let’s take a look at a slightly modified version of the extended example with two buttons._images/layout_box_example.png
First, we create a horizontally orientated box container where 6 pixels are placed between children. This box becomes the child of the top-level window.
Subsequently, we add two different buttons to the box container.
While with Gtk.Box.pack_start() widgets are positioned from left to right, Gtk.Box.pack_end() positions them from right to left.

### Grid

Gtk.Grid is a container which arranges its child widgets in rows and columns, but you do not need to specify the dimensions in the constructor. Children are added using Gtk.Grid.attach(). They can span multiple rows or columns. The Gtk.Grid.attach() method takes five parameters:
    The child parameter is the Gtk.Widget to add.
    left is the column number to attach the left side of child to.
    top indicates the row number to attach the top side of child to.
    width and height indicate the number of columns that the child will span, and the number of rows that the child will span, respectively.
It is also possible to add a child next to an existing child, using Gtk.Grid.attach_next_to(), which also takes five parameters:
    child is the Gtk.Widget to add, as above.
    sibling is an existing child widget of self (a Gtk.Grid instance) or None. The child widget will be placed next to sibling, or if sibling is None, at the beginning or end of the grid.
    side is a Gtk.PositionType indicating the side of sibling that child is positioned next to.
    width and height indicate the number of columns and rows the child widget will span, respectively.
Finally, Gtk.Grid can be used like a Gtk.Box by just using Gtk.Grid.add(), which will place children next to each other in the direction determined by the “orientation” property (defaults to Gtk.Orientation.HORIZONTAL).
6.2.1. Example
_images/layout_grid_example.png


### ListBox

A Gtk.ListBox is a vertical container that contains Gtk.ListBoxRow children. These rows can be dynamically sorted and filtered, and headers can be added dynamically depending on the row content. It also allows keyboard and mouse navigation and selection like a typical list.

Using Gtk.ListBox is often an alternative to Gtk.TreeView, especially when the list content has a more complicated layout than what is allowed by a Gtk.CellRenderer, or when the content is interactive (i.e. has a button in it).

Although a Gtk.ListBox must have only Gtk.ListBoxRow children, you can add any kind of widget to it via Gtk.Container.add() and a Gtk.ListBoxRow widget will automatically be inserted between the list and the widget.
6.3.1. Example
_images/listbox_example.png

### Stack and StackSwitcher

A Gtk.Stack is a container which only shows one of its children at a time. In contrast to Gtk.Notebook, Gtk.Stack does not provide a means for users to change the visible child. Instead, the Gtk.StackSwitcher widget can be used with Gtk.Stack to provide this functionality.

Transitions between pages can be animated as slides or fades. This can be controlled with Gtk.Stack.set_transition_type(). These animations respect the “gtk-enable-animations” setting.

Transition speed can be adjusted with Gtk.Stack.set_transition_duration()

The Gtk.StackSwitcher widget acts as a controller for a Gtk.Stack; it shows a row of buttons to switch between the various pages of the associated stack widget.

All the content for the buttons comes from the child properties of the Gtk.Stack.

It is possible to associate multiple Gtk.StackSwitcher widgets with the same Gtk.Stack widget.
6.4.1. Example
_images/stack_example.png

### HeaderBar
A Gtk.HeaderBar is similar to a horizontal Gtk.Box, it allows to place children at the start or the end. In addition, it allows a title to be displayed. The title will be centered with respect to the width of the box, even if the children at either side take up different amounts of space.

Since GTK+ now supports Client Side Decoration, a Gtk.HeaderBar can be used in place of the title bar (which is rendered by the Window Manager).

A Gtk.HeaderBar is usually located across the top of a window and should contain commonly used controls which affect the content below. They also provide access to window controls, including the close window button and window menu.
6.5.1. Example
_images/headerbar_example.png

### FlowBox

Note

This example requires at least GTK+ 3.12.

A Gtk.FlowBox is a container that positions child widgets in sequence according to its orientation.

For instance, with the horizontal orientation, the widgets will be arranged from left to right, starting a new row under the previous row when necessary. Reducing the width in this case will require more rows, so a larger height will be requested.

Likewise, with the vertical orientation, the widgets will be arranged from top to bottom, starting a new column to the right when necessary. Reducing the height will require more columns, so a larger width will be requested.

The children of a Gtk.FlowBox can be dynamically sorted and filtered.

Although a Gtk.FlowBox must have only Gtk.FlowBoxChild children, you can add any kind of widget to it via Gtk.Container.add(), and a Gtk.FlowBoxChild widget will automatically be inserted between the box and the widget.
6.6.1. Example
_images/flowbox_example.png

import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk, Gdk


class FlowBoxWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="FlowBox Demo")
        self.set_border_width(10)
        self.set_default_size(300, 250)

        header = Gtk.HeaderBar(title="Flow Box")
        header.set_subtitle("Sample FlowBox app")
        header.props.show_close_button = True

        self.set_titlebar(header)

        scrolled = Gtk.ScrolledWindow()
        scrolled.set_policy(Gtk.PolicyType.NEVER, Gtk.PolicyType.AUTOMATIC)

        flowbox = Gtk.FlowBox()
        flowbox.set_valign(Gtk.Align.START)
        flowbox.set_max_children_per_line(30)
        flowbox.set_selection_mode(Gtk.SelectionMode.NONE)

        self.create_flowbox(flowbox)

        scrolled.add(flowbox)

        self.add(scrolled)
        self.show_all()

    def on_draw(self, widget, cr, data):
        context = widget.get_style_context()

        width = widget.get_allocated_width()
        height = widget.get_allocated_height()
        Gtk.render_background(context, cr, 0, 0, width, height)

        r, g, b, a = data["color"]
        cr.set_source_rgba(r, g, b, a)
        cr.rectangle(0, 0, width, height)
        cr.fill()

    def color_swatch_new(self, str_color):
        rgba = Gdk.RGBA()
        rgba.parse(str_color)

        button = Gtk.Button()

        area = Gtk.DrawingArea()
        area.set_size_request(24, 24)
        area.connect("draw", self.on_draw, {"color": rgba})

        button.add(area)

        return button

    def create_flowbox(self, flowbox):
        colors = [
            "AliceBlue",
            "AntiqueWhite",
            "AntiqueWhite1",
            "AntiqueWhite2",
            "AntiqueWhite3",
            "AntiqueWhite4",
            "aqua",
            "aquamarine",
            "aquamarine1",
            "aquamarine2",
            "aquamarine3",
            "aquamarine4",
            "azure",
            "azure1",
            "azure2",
            "azure3",
            "azure4",
            "beige",
            "bisque",
            "bisque1",
            "bisque2",
            "bisque3",
            "bisque4",
            "black",
            "BlanchedAlmond",
            "blue",
            "blue1",
            "blue2",
            "blue3",
            "blue4",
            "BlueViolet",
            "brown",
            "brown1",
            "brown2",
            "brown3",
            "brown4",
            "burlywood",
            "burlywood1",
            "burlywood2",
            "burlywood3",
            "burlywood4",
            "CadetBlue",
            "CadetBlue1",
            "CadetBlue2",
            "CadetBlue3",
            "CadetBlue4",
            "chartreuse",
            "chartreuse1",
            "chartreuse2",
            "chartreuse3",
            "chartreuse4",
            "chocolate",
            "chocolate1",
            "chocolate2",
            "chocolate3",
            "chocolate4",
            "coral",
            "coral1",
            "coral2",
            "coral3",
            "coral4",
        ]

        for color in colors:
            button = self.color_swatch_new(color)
            flowbox.add(button)


win = FlowBoxWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()

6.7. Notebook

The Gtk.Notebook widget is a Gtk.Container whose children are pages that can be switched between using tab labels along one edge.

There are many configuration options for GtkNotebook. Among other things, you can choose on which edge the tabs appear (see Gtk.Notebook.set_tab_pos()), whether, if there are too many tabs to fit the notebook should be made bigger or scrolling arrows added (see Gtk.Notebook.set_scrollable(), and whether there will be a popup menu allowing the users to switch pages (see Gtk.Notebook.popup_enable(), Gtk.Notebook.popup_disable()).
6.7.1. Example
_images/notebook_plain_example.png

import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class MyWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="Simple Notebook Example")
        self.set_border_width(3)

        self.notebook = Gtk.Notebook()
        self.add(self.notebook)

        self.page1 = Gtk.Box()
        self.page1.set_border_width(10)
        self.page1.add(Gtk.Label(label="Default Page!"))
        self.notebook.append_page(self.page1, Gtk.Label(label="Plain Title"))

        self.page2 = Gtk.Box()
        self.page2.set_border_width(10)
        self.page2.add(Gtk.Label(label="A page with an image for a Title."))
        self.notebook.append_page(
            self.page2, Gtk.Image.new_from_icon_name("help-about", Gtk.IconSize.MENU)
        )


win = MyWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
