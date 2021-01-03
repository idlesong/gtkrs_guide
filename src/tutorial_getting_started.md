## getting started
### basic examples
[basic.rs](basic.rs), [basic_subclass](basic_subclass.rs), [sync_widgets](sync_widgets.rs)

### builders
Tutorial [builders](builders.rs),[builder_basics](builder_basics.rs),[builder_signal](builder_signal.rs)

### Glade
Glade is a tool which allows to easily write Gtk applications. Let’s see how you can use it with Gtk-rs.
Example

There isn’t much to explain in here. If you don’t know how to use Glade, take a look at their website directly. So first, let’s see a simple and short example:
```
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
```
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
```
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
```
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