## Getting started
To start with our tutorial we create the simplest program possible. This program will create an a window with a button.

There are two ways to build UIs with gtk: **the code way**, and **the builder way**(WYSIWYG way with glade).

### Build UI: code way
[basic.rs](basic.rs), [basic_subclass](basic_subclass.rs), [sync_widgets](sync_widgets.rs)

``` rust
extern crate gio;
extern crate gtk;

use gio::prelude::*;
use gtk::prelude::*;

use std::env::args;

fn build_ui(application: &gtk::Application) {
    let window = gtk::ApplicationWindow::new(application);

    window.set_title("First GTK+ Program");
    window.set_border_width(10);
    window.set_position(gtk::WindowPosition::Center);
    window.set_default_size(350, 70);

    let button = gtk::Button::new_with_label("Click me!");

    window.add(&button);

    window.show_all();
}

fn main() {
    let application =
        gtk::Application::new(Some("com.github.gtk-rs.examples.basic"), Default::default())
            .expect("Initialization failed...");

    application.connect_activate(|app| {
        build_ui(app);
    });

    application.run(&args().collect::<Vec<_>>());
}
```

### Build UI: WYSIWYG way - Builder

The gtk::Builder class offers you the opportunity to design user interfaces without writing a single line of code. This is possible through describing the interface by an XML file and then loading the XML description at runtime and create the objects automatically, which the Builder class does for you. For the purpose of not needing to write the XML manually the Glade application lets you create the user interface in a WYSIWYG (what you see is what you get) manner

This method has several advantages:
- Less code needs to be written.
- UI changes can be seen more quickly, so UIs are able to improve.
- Designers without programming skills can create and edit UIs.
- The description of the user interface is independent from the programming language being used.

There is still code required for handling interface changes triggered by the user, but Gtk.Builder allows you to focus on implementing that functionality.

[builder_basics](builder_basics.rs),[builder_signal](builder_signal.rs)

### Glade
Glade is a tool which allows to easily write Gtk applications. Let’s see how you can use it with Gtk-rs.
Example

There isn’t much to explain in here. If you don’t know how to use Glade, take a look at their website directly. So first, let’s see a simple and short example:
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<interface>
  <!-- interface-requires gtk+ 3.0 -->
  <object class="GtkWindow" id="window1">
    <property name="title" translatable="yes">Builder Basics</property>
    <property name="default_width">320</property>
    <property name="default_height">240</property>
    <child>
      <object class="GtkButton" id="button1">
        <property name="label" translatable="yes">Big Useless Button</property>
      </object>
    </child>
  </object>
  <object class="GtkMessageDialog" id="messagedialog1">
    <property name="can_focus">False</property>
    <property name="type_hint">dialog</property>
    <child internal-child="vbox">
      <object class="GtkBox" id="messagedialog-vbox1">
        <property name="name">msgdialog</property>
        <property name="width_request">300</property>
        <property name="can_focus">False</property>
        <property name="tooltip_markup" translatable="yes">Thank you for trying this example</property>
        <property name="resize_mode">immediate</property>
        <property name="orientation">vertical</property>
        <property name="spacing">2</property>
        <child internal-child="action_area">
          <object class="GtkButtonBox" id="messagedialog-action_area1">
            <property name="can_focus">False</property>
            <property name="layout_style">end</property>
            <child>
              <placeholder/>
            </child>
          </object>
          <packing>
            <property name="expand">False</property>
            <property name="fill">True</property>
            <property name="pack_type">end</property>
            <property name="position">0</property>
          </packing>
        </child>
        <child>
          <object class="GtkLabel" id="label2">
            <property name="visible">True</property>
            <property name="can_focus">False</property>
            <property name="label" translatable="yes">You have pressed the button</property>
            <property name="ellipsize">end</property>
            <property name="width_chars">40</property>
            <property name="lines">1</property>
          </object>
          <packing>
            <property name="expand">False</property>
            <property name="fill">True</property>
            <property name="position">2</property>
          </packing>
        </child>
      </object>
    </child>
  </object>
</interface>
```

So in this file, we created a Window containing a Button, as simple as that. It also created a MessageDialog containing a message and a Label. Like I said, quite simple.

Now let’s see how you can use this in your Rust code:
``` rust
// First we get the file content.
let glade_src = include_str!("builder_basics.glade");
// Then we call the Builder call.
let builder = gtk::Builder::from_string(glade_src);

// We start the gtk main loop.
gtk::main();

Simple isn’t it? However, just this code won’t show anything. You need to call show_all method on the Window. But for that, you need to get the Window first:

// Our window id is "window1".
let window: gtk::Window = builder.get_object("window1").unwrap();
window.show_all();
```

And that’s all. If you need to add signal handlings, you need to do the same. For example, we want to show the MessageDialog when the Button is clicked. Let’s add it:
``` rust
let button: gtk::Button = builder.get_object("button1").unwrap();
let dialog: gtk::MessageDialog = builder.get_object("messagedialog1").unwrap();

button.connect_clicked(move |_| {
    // We make the dialog window blocks all other windows.
    dialog.run();
    // When it finished running, we hide it again.
    dialog.hide();
});
```

Which gives us:
``` rust
if gtk::init().is_err() {
    println!("Failed to initialize GTK.");
    return;
}
let glade_src = include_str!("builder_basics.glade");
let builder = gtk::Builder::from_string(glade_src);

let window: gtk::Window = builder.get_object("window1").unwrap();
let button: gtk::Button = builder.get_object("button1").unwrap();
let dialog: gtk::MessageDialog = builder.get_object("messagedialog1").unwrap();

button.connect_clicked(move |_| {
    dialog.run();
    dialog.hide();
});

window.show_all();

gtk::main();
```
