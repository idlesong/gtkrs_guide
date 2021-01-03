## Buttons and Toggles
- [Button](https://gtk-rs.org/docs/gtk/struct.Button.html) — A widget that emits a signal when clicked on
- [CheckButton](https://gtk-rs.org/docs/gtk/struct.CheckButton.html) — Create widgets with a discrete toggle button
- [RadioButton](https://gtk-rs.org/docs/gtk/struct.RadioButton.html) — A choice from multiple check buttons
- [ToggleButton](https://gtk-rs.org/docs/gtk/struct.ToggleButton.html) — Create buttons which retain their state
- [LinkButton](https://gtk-rs.org/docs/gtk/struct.LinkButton.html) — Create buttons bound to a URL
- [MenuButton](https://gtk-rs.org/docs/gtk/struct.MenuButton.html) — A widget that shows a popup when clicked on
- [Switch](https://gtk-rs.org/docs/gtk/struct.Switch.html) — A “light switch” style toggle
- [ScaleButton](https://gtk-rs.org/docs/gtk/struct.ScaleButton.html) — A button which pops up a scale
- [VolumeButton](https://gtk-rs.org/docs/gtk/struct.VolumeButton.html) — A button which pops up a volume control
- [LockButton](https://gtk-rs.org/docs/gtk/struct.LockButton.html) — A widget to unlock or lock privileged operations
- [ModelButton](https://gtk-rs.org/docs/gtk/struct.ModelButton.html) — A button that uses a GAction as model

### Button

The Button widget is another commonly used widget. It is generally used to attach a function that is called when the button is pressed.

The Gtk.Button widget can hold any valid child widget. That is it can hold most any other standard Gtk.Widget. The most commonly used child is the Gtk.Label.

Usually, you want to connect to the button’s “clicked” signal which is emitted when the button has been pressed and released.
9.1.1. Example

### ToggleButton

A Gtk.ToggleButton is very similar to a normal Gtk.Button, but when clicked they remain activated, or pressed, until clicked again. When the state of the button is changed, the “toggled” signal is emitted.

To retrieve the state of the Gtk.ToggleButton, you can use the Gtk.ToggleButton.get_active() method. This returns True if the button is “down”. You can also set the toggle button’s state, with Gtk.ToggleButton.set_active(). Note that, if you do this, and the state actually changes, it causes the “toggled” signal to be emitted.
9.2.1. Example
_images/togglebutton_example.png


### CheckButton

Gtk.CheckButton inherits from Gtk.ToggleButton. The only real difference between the two is Gtk.CheckButton’s appearance. A Gtk.CheckButton places a discrete Gtk.ToggleButton next to a widget, (usually a Gtk.Label). The “toggled” signal, Gtk.ToggleButton.set_active() and Gtk.ToggleButton.get_active() are inherited.

### RadioButton

Like checkboxes, radio buttons also inherit from Gtk.ToggleButton, but these work in groups, and only one Gtk.RadioButton in a group can be selected at any one time. Therefore, a Gtk.RadioButton is one way of giving the user a choice from many options.

Radio buttons can be created with one of the static methods Gtk.RadioButton.new_from_widget(), Gtk.RadioButton.new_with_label_from_widget() or Gtk.RadioButton.new_with_mnemonic_from_widget(). The first radio button in a group will be created passing None as the group argument. In subsequent calls, the group you wish to add this button to should be passed as an argument.

When first run, the first radio button in the group will be active. This can be changed by calling Gtk.ToggleButton.set_active() with True as first argument.

Changing a Gtk.RadioButton’s widget group after its creation can be achieved by calling Gtk.RadioButton.join_group().
9.4.1. Example
