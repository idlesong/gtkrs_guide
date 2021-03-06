## Buttons and Toggles

### Button
 — _A widget that emits a signal when clicked on_ [Button](https://gtk-rs.org/docs/gtk/struct.Button.html) ![button](images/gtkrs_button.png)

The Button widget is another commonly used widget. It is generally used to attach a function that is called when the button is clicked.

The Gtk.Button widget can hold any valid child widget. That is it can hold most any other standard Gtk.Widget. The most commonly used child is the Gtk.Label.

Usually, you want to connect to the button’s “clicked” signal which is emitted when the button has been pressed and released.

``` xml
<!-- build UI, builder way -->
<object class="GtkButton" id="button">
  <property name="label" translatable="yes">button</property>
  <property name="visible">True</property>
  <property name="can_focus">True</property>
  <property name="receives_default">True</property>
  <property name="image">image2</property>
</object>
```
``` rust
// get UI widget from ui file
let builder = Builder::new_from_string("builder.ui");
let button: Button = builder.get_object("button").expect("Couldn't get button");

# // build UI, code_way
# let button = gtk::Button::new_with_label("Click me!");
button.connect_clicked(|but| {
    println!("button");
});
```

### ToggleButton
[ToggleButton](https://gtk-rs.org/docs/gtk/struct.ToggleButton.html) — _Create buttons which retain their state_ ![ToggleButton](images/gtkrs_toggle_button.png)

A Gtk.ToggleButton is very similar to a normal Gtk.Button, but when clicked they remain activated, or pressed, until clicked again. When the state of the button is changed, the “toggled” signal is emitted.

To retrieve the state of the Gtk.ToggleButton, you can use the Gtk.ToggleButton.get_active() method. This returns True if the button is “down”. You can also set the toggle button’s state, with Gtk.ToggleButton.set_active(). Note that, if you do this, and the state actually changes, it causes the “toggled” signal to be emitted.
``` xml
<object class="GtkToggleButton" id="toggle_button">
  <property name="label" translatable="yes">Toggle Me !</property>
  <property name="visible">True</property>
  <property name="can_focus">True</property>
  <property name="receives_default">True</property>
</object>
```

``` rust
let toggle_button = gtk::ToggleButton::new_with_label("toggle");
toggle_button.set_active(true);
toggle_button.connect_clicked(|toggle| {
    println!("toggle clicked");
});
```

### CheckButton
  — _Create widgets with a discrete toggle button_ [CheckButton](https://gtk-rs.org/docs/gtk/struct.CheckButton.html) ![CheckButton](images/gtkrs_check_button.png)

Gtk.CheckButton inherits from Gtk.ToggleButton. The only real difference between the two is Gtk.CheckButton’s appearance. A Gtk.CheckButton places a discrete Gtk.ToggleButton next to a widget, (usually a Gtk.Label). The “toggled” signal, Gtk.ToggleButton.set_active() and Gtk.ToggleButton.get_active() are inherited.
``` xml
<object class="GtkCheckButton" id="check_button">
  <property name="label" translatable="yes">checkbutton</property>
  <property name="visible">True</property>
  <property name="can_focus">True</property>
  <property name="receives_default">False</property>
  <property name="xalign">0</property>
  <property name="draw_indicator">True</property>
</object>
```

``` rust
// get UI widget from ui file
let builder = Builder::new_from_string("builder.ui");
let check_button: Button = builder.get_object("check_button").expect("Couldn't get button");

# // build UI, code_way
# let check_button = gtk::CheckButton::new_with_label("Click me!");

check_button.connect_clicked(|but| {
    println!("button");
});
```

### RadioButton
 — _Create widgets with a discrete toggle button_  [RadioButton](https://gtk-rs.org/docs/gtk/struct.RadioButton.html)  ![RadioButton](images/gtkrs_radio_button.png)

Like checkboxes, radio buttons also inherit from Gtk.ToggleButton, but these work in groups, and only one Gtk.RadioButton in a group can be selected at any one time. Therefore, a Gtk.RadioButton is one way of giving the user a choice from many options.

Radio buttons can be created with one of the static methods Gtk.RadioButton.new_from_widget(), Gtk.RadioButton.new_with_label_from_widget() or Gtk.RadioButton.new_with_mnemonic_from_widget(). The first radio button in a group will be created passing None as the group argument. In subsequent calls, the group you wish to add this button to should be passed as an argument.

When first run, the first radio button in the group will be active. This can be changed by calling Gtk.ToggleButton.set_active() with True as first argument.

Changing a Gtk.RadioButton’s widget group after its creation can be achieved by calling Gtk.RadioButton.join_group().

``` rust
let radio_button = gtk::RadioButton::new_with_label("radio_button");
radio_button.connect_clicked(|radio| {
    // radio.set_active(radio.get_active());
    println!("radio clicked");
});
hbox.pack_start(&radio_button, false, false, 0);
```

### LinkButton
 — _Create buttons bound to a URL_ [LinkButton](https://gtk-rs.org/docs/gtk/struct.LinkButton.html)  ![LinkButton](images/gtkrs_link_button.png)

A Gtk.LinkButton is a Gtk.Button with a hyperlink, similar to the one used by web browsers, which triggers an action when clicked. It is useful to show quick links to resources.

The URI bound to a Gtk.LinkButton can be set specifically using Gtk.LinkButton.set_uri(), and retrieved using Gtk.LinkButton.get_uri().
``` xml
<object class="GtkLinkButton" id="link_button">
  <property name="label" translatable="yes">rust-lang.org</property>
  <property name="visible">True</property>
  <property name="can_focus">True</property>
  <property name="receives_default">True</property>
  <property name="relief">none</property>
  <property name="uri">https://www.rust-lang.org/</property>
</object>
```

``` rust
let link_button = gtk::LinkButton::new_with_label(
    "https://www.gtk.org",
    Some("GTK+ Homepage")
);
```

### Switch
 — _A “light switch” style toggle_ [Switch](https://gtk-rs.org/docs/gtk/struct.Switch.html) ![Switch](images/gtkrs_switch_button.png)

A Gtk.Switch is a widget that has two states: on or off. The user can control which state should be active by clicking the empty area, or by dragging the handle.

You shouldn’t use the “activate” signal on the Gtk.Switch which is an action signal and emitting it causes the switch to animate. Applications should never connect to this signal, but use the “notify::active” signal, see the example here below.

``` xml
<object class="GtkSwitch" id="switch">
  <property name="visible">True</property>
  <property name="can_focus">True</property>
</object>
```

``` rust
switch.connect_property_active_notify(|switch| {
    let mut state = "on";
    if switch.get_active() {
        state = "on";
    } else{
        state = "off";
    }
    println!("Switch was turned {}", state);
});
switch.set_active(false);
```


#### buttons and toggles example
![buttons and toggles](images/buttons_toggles.png)


``` rust
extern crate gio;
extern crate gtk;

use gio::prelude::*;
use gtk::prelude::*;

use std::env::args;

fn build_ui(application: &gtk::Application) {
    let window = gtk::ApplicationWindow::new(application);

    window.set_title("Buttons and Toggles");
    window.set_border_width(10);
    window.set_position(gtk::WindowPosition::Center);
    window.set_default_size(350, 48);

    let button = gtk::Button::new_with_label("Click me!");
    button.connect_clicked(|but| {
        println!("button");
    });
    // Stack the buttons horizontally
    let hbox = gtk::Box::new(gtk::Orientation::Vertical, 0);
    hbox.pack_start(&button, true, true, 0);

    let toggle_button = gtk::ToggleButton::new_with_label("toggle");
    toggle_button.set_active(true);
    toggle_button.connect_clicked(|toggle| {
        println!("toggle clicked");
    });
    hbox.pack_start(&toggle_button, true, true, 0);

    let radio_button = gtk::RadioButton::new_with_label("radio_button");
    radio_button.connect_clicked(|radio| {
        // radio.set_active(radio.get_active());
        println!("radio clicked");
    });
    hbox.pack_start(&radio_button, false, false, 0);

    let radio_button2 = gtk::RadioButton::new_with_label("radio_button2");
    radio_button2.connect_clicked(|radio| {
        // radio.set_active(radio.get_active());
        println!("radio clicked");
    });
    hbox.pack_start(&radio_button2, false, false, 0);

    let link_button = gtk::LinkButton::new_with_label(
        "https://www.gtk.org",
        Some("GTK+ Homepage")
    );
    hbox.pack_start(&link_button, false, false, 0);

    let switch = gtk::Switch::new();
    switch.connect_property_active_notify(|switch| {
        let mut state = "on";
        if switch.get_active() {
            state = "on";
        } else{
            state = "off";
        }
        println!("Switch was turned {}", state);
    });
    switch.set_active(false);
    hbox.pack_start(&switch, false, false, 0);

    window.add(&hbox);

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

### Common button and toggle widgets list
widgets | description
 ---|---
![alt text](./images/gtkrs_button.png) | [Button](https://gtk-rs.org/docs/gtk/struct.Button.html) — A widget that emits a signal when clicked on
![alt text](./images/gtkrs_check_button.png) | [CheckButton](https://gtk-rs.org/docs/gtk/struct.CheckButton.html) — Create widgets with a discrete toggle button
![alt text](./images/radio-group.png) | [RadioButton](https://gtk-rs.org/docs/gtk/struct.RadioButton.html) — A choice from multiple check buttons
![alt text](./images/gtkrs_toggle_button.png) | [ToggleButton](https://gtk-rs.org/docs/gtk/struct.ToggleButton.html) — Create buttons which retain their state
![alt text](./images/gtkrs_link_button.png) | [LinkButton](https://gtk-rs.org/docs/gtk/struct.LinkButton.html) — Create buttons bound to a URL
![alt text](./images/menu-button.png) | [MenuButton](https://gtk-rs.org/docs/gtk/struct.MenuButton.html) — A widget that shows a popup when clicked on
- | [Switch](https://gtk-rs.org/docs/gtk/struct.Switch.html) — A “light switch” style toggle
- | [ScaleButton](https://gtk-rs.org/docs/gtk/struct.ScaleButton.html) — A button which pops up a scale
![alt text](./images/volumebutton.png) | [VolumeButton](https://gtk-rs.org/docs/gtk/struct.VolumeButton.html) — A button which pops up a volume control
![alt text](./images/lockbutton.png) | [LockButton](https://gtk-rs.org/docs/gtk/struct.LockButton.html) — A widget to unlock or lock privileged operations
- | [ModelButton](https://gtk-rs.org/docs/gtk/struct.ModelButton.html) — A button that uses a GAction as model
