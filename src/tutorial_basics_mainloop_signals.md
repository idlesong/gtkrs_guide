# Basic: Main Loop and Signals
## Main loop and Signals

Like most GUI toolkits, GTK+ uses an event-driven programming model. When the user is doing nothing, GTK+ sits in the main loop and waits for input. If the user performs some action - say, a mouse click - then the main loop “wakes up” and delivers an event to GTK+.

When widgets receive an event, they frequently emit one or more signals. Signals notify your program that “something interesting happened” by invoking functions you’ve connected to the signal. Such functions are commonly known as callbacks. When your callbacks are invoked, you would typically take some action - for example, when an Open button is clicked you might display a file chooser dialog. After a callback finishes, GTK+ will return to the main loop and await more user input.

A generic example is:
```handler_id = widget.connect("event", callback, data)```

Firstly, widget is an instance of a widget we created earlier. Next, the event we are interested in. Each widget has its own particular events which can occur. For instance, if you have a button you usually want to connect to the “clicked” event. This means that when the button is clicked, the signal is issued. Thirdly, the callback argument is the name of the callback function. It contains the code which runs when signals of the specified type are issued. Finally, the data argument includes any data which should be passed when the signal is issued. However, this argument is completely optional and can be left out if not required.

The function returns a number that identifies this particular signal-callback pair. It is required to disconnect from a signal such that the callback function will not be called during any future or currently ongoing emissions of the signal it has been connected to.

```widget.disconnect(handler_id)```

If you have lost the “handler_id” for some reason (for example the handlers were installed using Gtk.Builder.connect_signals()), you can still disconnect a specific callback using the function disconnect_by_func():

```widget.disconnect_by_func(callback)```

Applications should connect to the “destroy” signal of the top-level window. It is emitted when an object is destroyed, so when a user requests that a toplevel window is closed, the default handler for this signal destroys the window, but does not terminate the application. Connecting the “destroy” signal of the top-level window to the function Gtk.main_quit() will result in the desired behaviour.

```
window.connect("destroy", Gtk.main_quit)
```

Calling Gtk.main_quit() makes the main loop inside of Gtk.main() return.

## Callbacks and closures

It’s very common in GUI libraries to have callbacks (or equivalent) in order to perform an action when a specific event happens. Let’s see how you can do it with Gtk-rs.

#### Closures!

Closures, unlike functions-pointer, keep their environment, which is very useful to not have to send any argument you need into it. However, a closure’s lifetime is difficult to track. In Gtk-rs, it requires a static lifetime to be sure that any objects captured by the closure will still be alive, whatever the moment the closure is invoked.

Now that you have all information, let’s take a look to an example:

In C, youll write:
```
#include <gtk/gtk.h>

void callback_clicked(GtkWidget *widget, gpointer data) {
    gtk_button_set_label(GTK_BUTTON(widget), "Window");
}

GtkWidget *button = gtk_button_new_with_label("Click me!");
g_signal_connect(button, "clicked", G_CALLBACK(callback_clicked), NULL);
```
It now becomes:
```
use gtk::{Button, ButtonExt};

let button = Button::with_label("Click me!");
button.connect_clicked(|but| {
    but.set_label("I've been clicked!");
});
```

As simple as that! Now comes the less funny part. Let’s say you want to update another widget when the button is clicked and use it after:

```
use gtk::{Box, Button, ButtonExt, ContainerExt, WidgetExt};

// First we create a layout.
let container = Box::new(gtk::Orientation::Vertical, 5);
// the label which will be modified inside the closure.
let label = gtk::Label::new("");
let button = Button::with_label("Click me!");
button.connect_clicked(move |_| {
    label.set_label("Button has been clicked!");
});

container.add(&button);
container.add(&label);
```

If you try to compile this code, you’ll get the following error:

error[E0382]: use of moved value: `label`

To make it work, just clone label before sending it into the closure:
```
use gtk::{Box, Button, ButtonExt, ContainerExt, WidgetExt};

// First we create a layout.
let container = Box::new(gtk::Orientation::Vertical, 5);
// the label which will be modified inside the closure.
let label = gtk::Label::new("");
let button = Button::with_label("Click me!");
// We clone label so we can send it into the closure.
let label_clone = label.clone();
button.connect_clicked(move |_| {
    label_clone.set_label("Button has been clicked!");
});

container.add(&button);
container.add(&label);
```
Now it works, as simple as that! Remember: cloning a Gtk-rs object only costs a pointer copy, so it’s not a problem.
Using non-Gtk-rs object into a Gtk-rs closure

That’s where things get a bit more complicated. Let’s say you want to write a multi-window program and want to keep track of your windows so you can access them from multiple closures.

One way to do it is using Rc and RefCell structs from Rust standard library. Now let’s see this into action in a short example:
```
use gtk::{Button, ButtonExt, Window};

use std::cell::RefCell;
use std::collections::HashMap;
use std::rc::Rc;

let windows: Rc<RefCell<HashMap<usize, Window>>> = Rc::new(RefCell::new(HashMap::new()));
let button = Button::with_label("Click me!");
// We copy the reference to the cell containing the hashmap.
let windows_clone = windows.clone();
button.connect_clicked(move |_| {
    // create_window functions creates a window and return the following tuple: (usize, Window).
    let (window_id, window) = create_window();
    windows_clone.borrow_mut().unwrap().insert(window_id, window);
});

 ...

another_button.connect_clicked(move |_| {
    let id_to_remove = get_id_to_remove();
    windows.borrow_mut().unwrap().remove(&id_to_remove);
});
```

A bit annoying to write. To give a simple explanation on how Rc<RefCell<T>> works:
```
    Rc is just a reference counter, so it keeps count of the number of instances of the object it holds and then drop it and there is no more reference.
    RefCell is a bit more complicated. It allows to make an object mutable when/where it shouldn’t. For more information, take a look at its documentation.
```

However, a macro can make your life a bit easier to do this (you can take a look at the code but it’s not mandatory to understand how it works):
```
macro_rules! clone {
    (@param _) => ( _ );
    (@param $x:ident) => ( $x );
    ($($n:ident),+ => move || $body:expr) => (
        {
            $( let $n = $n.clone(); )+
            move || $body
        }
    );
    ($($n:ident),+ => move |$($p:tt),+| $body:expr) => (
        {
            $( let $n = $n.clone(); )+
            move |$(clone!(@param $p),)+| $body
        }
    );
}
```

And then you can use it as follow:

```
let windows: Rc<RefCell<HashMap<usize, Window>>> = Rc::new(RefCell::new(HashMap::new()));
button.connect_clicked(clone!(windows => move |_| {
    let (window_id, window) = create_window();
    windows.borrow_mut().unwrap().insert(window_id, window);
}));
```
