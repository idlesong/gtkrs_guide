## CellRenderers
Gtk.CellRenderer widgets are used to display information within widgets such as the Gtk.TreeView or Gtk.ComboBox. They work closely with the associated widgets and are very powerful, with lots of configuration options for displaying a large amount of data in different ways. There are seven Gtk.CellRenderer widgets which can be used for different purposes:

-        Gtk.CellRendererText
-        Gtk.CellRendererToggle
-        Gtk.CellRendererPixbuf
-        Gtk.CellRendererCombo
-        Gtk.CellRendererProgress
-        Gtk.CellRendererSpinner
-        Gtk.CellRendererSpin
-        Gtk.CellRendererAccel

### 14.1. CellRendererText

A Gtk.CellRendererText renders a given text in its cell, using the font, color and style information provided by its properties. The text will be ellipsized if it is too long and the “ellipsize” property allows it.

By default, text in Gtk.CellRendererText widgets is not editable. This can be changed by setting the value of the “editable” property to True:

cell.set_property("editable", True)

You can then connect to the “edited” signal and update your Gtk.TreeModel accordingly.

#### 14.1.1. Example
``` rust
_images/cellrenderertext_example.png

import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class CellRendererTextWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererText Example")

        self.set_default_size(200, 200)

        self.liststore = Gtk.ListStore(str, str)
        self.liststore.append(["Fedora", "https://fedoraproject.org/"])
        self.liststore.append(["Slackware", "http://www.slackware.com/"])
        self.liststore.append(["Sidux", "http://sidux.com/"])

        treeview = Gtk.TreeView(model=self.liststore)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Text", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_editabletext = Gtk.CellRendererText()
        renderer_editabletext.set_property("editable", True)

        column_editabletext = Gtk.TreeViewColumn(
            "Editable Text", renderer_editabletext, text=1
        )
        treeview.append_column(column_editabletext)

        renderer_editabletext.connect("edited", self.text_edited)

        self.add(treeview)

    def text_edited(self, widget, path, text):
        self.liststore[path][1] = text


win = CellRendererTextWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```

### 14.2. CellRendererToggle

Gtk.CellRendererToggle renders a toggle button in a cell. The button is drawn as a radio- or checkbutton, depending on the “radio” property. When activated, it emits the “toggled” signal.

As a Gtk.CellRendererToggle can have two states, active and not active, you most likely want to bind the “active” property on the cell renderer to a boolean value in the model, thus causing the check button to reflect the state of the model.

#### 14.2.1. Example
``` rust
_images/cellrenderertoggle_example.png

import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class CellRendererToggleWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererToggle Example")

        self.set_default_size(200, 200)

        self.liststore = Gtk.ListStore(str, bool, bool)
        self.liststore.append(["Debian", False, True])
        self.liststore.append(["OpenSuse", True, False])
        self.liststore.append(["Fedora", False, False])

        treeview = Gtk.TreeView(model=self.liststore)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Text", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_toggle = Gtk.CellRendererToggle()
        renderer_toggle.connect("toggled", self.on_cell_toggled)

        column_toggle = Gtk.TreeViewColumn("Toggle", renderer_toggle, active=1)
        treeview.append_column(column_toggle)

        renderer_radio = Gtk.CellRendererToggle()
        renderer_radio.set_radio(True)
        renderer_radio.connect("toggled", self.on_cell_radio_toggled)

        column_radio = Gtk.TreeViewColumn("Radio", renderer_radio, active=2)
        treeview.append_column(column_radio)

        self.add(treeview)

    def on_cell_toggled(self, widget, path):
        self.liststore[path][1] = not self.liststore[path][1]

    def on_cell_radio_toggled(self, widget, path):
        selected_path = Gtk.TreePath(path)
        for row in self.liststore:
            row[2] = row.path == selected_path


win = CellRendererToggleWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```

### 14.3. CellRendererPixbuf

A Gtk.CellRendererPixbuf can be used to render an image in a cell. It allows to render either a given Gdk.Pixbuf (set via the “pixbuf” property) or a named icon (set via the “icon-name” property).

#### 14.3.1. Example
_images/cellrendererpixbuf_example.png
``` rust
import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class CellRendererPixbufWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererPixbuf Example")

        self.set_default_size(200, 200)

        self.liststore = Gtk.ListStore(str, str)
        self.liststore.append(["New", "document-new"])
        self.liststore.append(["Open", "document-open"])
        self.liststore.append(["Save", "document-save"])

        treeview = Gtk.TreeView(model=self.liststore)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Text", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_pixbuf = Gtk.CellRendererPixbuf()

        column_pixbuf = Gtk.TreeViewColumn("Image", renderer_pixbuf, icon_name=1)
        treeview.append_column(column_pixbuf)

        self.add(treeview)


win = CellRendererPixbufWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```

### 14.4. CellRendererCombo

Gtk.CellRendererCombo renders text in a cell like Gtk.CellRendererText from which it is derived. But while the latter offers a simple entry to edit the text, Gtk.CellRendererCombo offers a Gtk.ComboBox widget to edit the text. The values to display in the combo box are taken from the Gtk.TreeModel specified in the “model” property.

The combo cell renderer takes care of adding a text cell renderer to the combo box and sets it to display the column specified by its “text-column” property.

A Gtk.CellRendererCombo can operate in two modes. It can be used with and without an associated Gtk.Entry widget, depending on the value of the
“has-entry” property.

#### 14.4.1. Example
_images/cellrenderercombo_example.png
``` rust
import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class CellRendererComboWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererCombo Example")

        self.set_default_size(200, 200)

        liststore_manufacturers = Gtk.ListStore(str)
        manufacturers = ["Sony", "LG", "Panasonic", "Toshiba", "Nokia", "Samsung"]
        for item in manufacturers:
            liststore_manufacturers.append([item])

        self.liststore_hardware = Gtk.ListStore(str, str)
        self.liststore_hardware.append(["Television", "Samsung"])
        self.liststore_hardware.append(["Mobile Phone", "LG"])
        self.liststore_hardware.append(["DVD Player", "Sony"])

        treeview = Gtk.TreeView(model=self.liststore_hardware)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Text", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_combo = Gtk.CellRendererCombo()
        renderer_combo.set_property("editable", True)
        renderer_combo.set_property("model", liststore_manufacturers)
        renderer_combo.set_property("text-column", 0)
        renderer_combo.set_property("has-entry", False)
        renderer_combo.connect("edited", self.on_combo_changed)

        column_combo = Gtk.TreeViewColumn("Combo", renderer_combo, text=1)
        treeview.append_column(column_combo)

        self.add(treeview)

    def on_combo_changed(self, widget, path, text):
        self.liststore_hardware[path][1] = text


win = CellRendererComboWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```

### 14.5. CellRendererProgress

Gtk.CellRendererProgress renders a numeric value as a progress bar in a cell. Additionally, it can display a text on top of the progress bar.

The percentage value of the progress bar can be modified by changing the “value” property. Similar to Gtk.ProgressBar, you can enable the activity mode by incrementing the “pulse” property instead of the “value” property.

#### 14.5.1. Example
_images/cellrendererprogress_example.png

``` rust
import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk, GLib


class CellRendererProgressWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererProgress Example")

        self.set_default_size(200, 200)

        self.liststore = Gtk.ListStore(str, int, bool)
        self.current_iter = self.liststore.append(["Sabayon", 0, False])
        self.liststore.append(["Zenwalk", 0, False])
        self.liststore.append(["SimplyMepis", 0, False])

        treeview = Gtk.TreeView(model=self.liststore)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Text", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_progress = Gtk.CellRendererProgress()
        column_progress = Gtk.TreeViewColumn(
            "Progress", renderer_progress, value=1, inverted=2
        )
        treeview.append_column(column_progress)

        renderer_toggle = Gtk.CellRendererToggle()
        renderer_toggle.connect("toggled", self.on_inverted_toggled)
        column_toggle = Gtk.TreeViewColumn("Inverted", renderer_toggle, active=2)
        treeview.append_column(column_toggle)

        self.add(treeview)

        self.timeout_id = GLib.timeout_add(100, self.on_timeout, None)

    def on_inverted_toggled(self, widget, path):
        self.liststore[path][2] = not self.liststore[path][2]

    def on_timeout(self, user_data):
        new_value = self.liststore[self.current_iter][1] + 1
        if new_value > 100:
            self.current_iter = self.liststore.iter_next(self.current_iter)
            if self.current_iter is None:
                self.reset_model()
            new_value = self.liststore[self.current_iter][1] + 1

        self.liststore[self.current_iter][1] = new_value
        return True

    def reset_model(self):
        for row in self.liststore:
            row[1] = 0
        self.current_iter = self.liststore.get_iter_first()


win = CellRendererProgressWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```

### 14.6. CellRendererSpin

Gtk.CellRendererSpin renders text in a cell like Gtk.CellRendererText from which it is derived. But while the latter offers a simple entry to edit the text, Gtk.CellRendererSpin offers a Gtk.SpinButton widget. Of course, that means that the text has to be parseable as a floating point number.

The range of the spinbutton is taken from the adjustment property of the cell renderer, which can be set explicitly or mapped to a column in the tree model, like all properties of cell renders. Gtk.CellRendererSpin also has properties for the climb rate and the number of digits to display.

#### 14.6.1. Example
_images/cellrendererspin_example.png

```
import gi

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk


class CellRendererSpinWindow(Gtk.Window):
    def __init__(self):
        Gtk.Window.__init__(self, title="CellRendererSpin Example")

        self.set_default_size(200, 200)

        self.liststore = Gtk.ListStore(str, int)
        self.liststore.append(["Oranges", 5])
        self.liststore.append(["Apples", 4])
        self.liststore.append(["Bananas", 2])

        treeview = Gtk.TreeView(model=self.liststore)

        renderer_text = Gtk.CellRendererText()
        column_text = Gtk.TreeViewColumn("Fruit", renderer_text, text=0)
        treeview.append_column(column_text)

        renderer_spin = Gtk.CellRendererSpin()
        renderer_spin.connect("edited", self.on_amount_edited)
        renderer_spin.set_property("editable", True)

        adjustment = Gtk.Adjustment(
            value=0,
            lower=0,
            upper=100,
            step_increment=1,
            page_increment=10,
            page_size=0,
        )
        renderer_spin.set_property("adjustment", adjustment)

        column_spin = Gtk.TreeViewColumn("Amount", renderer_spin, text=1)
        treeview.append_column(column_spin)

        self.add(treeview)

    def on_amount_edited(self, widget, path, value):
        self.liststore[path][1] = int(value)


win = CellRendererSpinWindow()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
```
