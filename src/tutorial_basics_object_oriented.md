# Basics: Object Oriented GTK & rust
## Objects
First thing to note (it’s very important!) is that the Gtk-rs objects can be cloned and it costs nothing more than copying a pointer, so basically nothing. The reason is quite simple (and I suppose you already guessed it): it’s simply because Gtk-rs structs only contains a pointer to the corresponding Gnome objects.

Now: why is cloning safe? One thing to note before going any further: it’s not thread safe (and you shouldn’t try to call a Gnome library function inside another thread). Otherwise, when a struct is dropped, it calls internally the g_object_unref function and calls the g_object_ref function when you call clone().

To put it simply: Gnome handles the resources allocation/removal for us.
Trait hierarchy

In Gtk, there is a widget hierarchy. In Rust, it’s implemented through “traits inheritance” and enforced by the compiler at compile-time. So, what does that mean exactly? Let’s take an example:

You have a Button. As says the gnome documentation, a Button inheritance tree (a bit simplified) looks like this:
```
 GObject
  ╰── GtkWidget
       ╰── GtkContainer
            ╰── GtkBin
                 ╰── GtkButton
```
Which means that a Button can use methods from any of its parents.

So basically, you just need to import a parent’s trait to be able to use its methods:
```
// we import Widget's methods.
use gtk::WidgetExt;

// we create a button
let button = gtk::Button::with_label("Click me!");

// we use the method from the widget
button.show_all();
```
As easy as that!

## Interfaces

The same goes for interfaces. The gnome documentation also says that a Button implements the following interfaces: GtkBuildable, GtkActionable and GtkActivatable. Just like parents’ methods, import the corresponding interface and then you’ll be able to use the methods.

I think that with this, you’ll be able to write anything you want without too much difficulties. Now it’s time to go deeper into Gtk-rs usage!

## Object-oriented Rust

Since there is an inheritance system in Gtk, it’s only logical to have one as well in Gtk-rs. Normally, most people won’t need this, but understanding how things work can help navigating the documentation a lot.

Each GTK class is split into a struct named after that class, and a trait with the same name and the suffix Ext, see for example WidgetExt. All methods except the constructor(s) are not in the struct, but in that trait. In addition, some other methods can be found in a …ExtManual trait, as seen in WidgetExtManual. This happens for implementation reasons currently. The same principle applies to GTK interfaces as well (have a look at the Orientable interface for an example). There are a few exceptional classes that don’t follow this general pattern: one reason for this is that final classes don’t need an extension trait because there can’t be any subclasses of them, and thus can have their methods defined on the struct itself.

## Basic inheritance

Any struct not only implements its Ext trait, but also all traits of its super classes. That way you can call methods of super classes directly on a struct.

The IsA trait is used to model the subtype relation of classes between structs. Every struct implements IsA<SuperClass> for each of its parent classes (and its implemented interfaces). For example FlowBox implements IsA<Buildable>, IsA<Container>, IsA<Orientable>, IsA<Widget>.

Passing classes as arguments is pretty straightforward. The only rule is that when accepting a class as function argument, take a generic IsA<ClassThatIWant> instead: fn add<P: IsA<Widget>>(&self, widget: &P). Now the method can be not only called with structs of that type, but also with structs of any subtype (in this case, any Widget).

## Upcasting
Upcasting should rarely be necessary due to the subtyping, but sometimes you need a “proper” Widget struct (instead of a WidgetExt implementor or an IsA<Widget>). This is actually quite simple to achieve:
```
let button = gtk::Button::with_label("Click me!");
let widget = button.upcast::<gtk::Widget>();
```

Since the Button struct implements IsA<Widget>, we can upcast into a Widget. It’s important to note that the IsA trait is implemented on every widget for every of its parents, which, in here, allows to upcast the Button into a Widget.

Let’s see now a more global usage.
## Checking if a widget is another widget

Let’s say you want to write a generic function and want to check if a Widget is actually a Box. First, let’s see a bit of code:

fn is_a_box<W: IsA<gtk::Object> + IsA<gtk::Widget> + Clone>(widget: &W) -> bool {
    widget.clone().upcast::<gtk::Widget>().is::<gtk::Box>()
}

Ok, so what’s happening in there? First, you’ll note the usage of the IsA trait. The received widget needs to implement both IsA<Widget> and IsA<Object>.

We need the Object to be able to use the Cast trait which contains both upcast and downcast methods (take a look to it for other methods as well).

We don’t really need our widget to be a Widget, we just put it here to make things easier (so we can upcast into a Widget without troubles).

So the point of this function is to upcast the widget to the highest widget type and then try downcasting it into the wanted object. We could make even more generic like this:

fn is_a<W: IsA<gtk::Object> + IsA<gtk::Widget> + Clone,
        T: IsA<gtk::Object> + IsA<gtk::Widget>>(widget: &W) -> bool {
    widget.clone().upcast::<gtk::Widget>().downcast::<T>().is_ok()
}

Then let’s test it:
```
let button = gtk::Button::with_label("Click me!");

assert_eq!(is_a::<_, gtk::Container>(&button), true);
assert_eq!(is_a::<_, gtk::Label>(&button), false);
```

### Gnome libraries and Rust

Currently, the Gtk-rs organization provides the bindings for the following libraries:
- Gtk (the widget toolkit)
- Gdk (low-level functions provided by the underlying windowing and graphics systems)
- Gdk-pixbuf (image loading and manipulation)
- Cairo (vector graphic API)
- Glib (data structures and utilities for dealing with them)
- Gio (file system abstractions)
- Pango (layout engine, text and font handling)

The goal is to provide a safe abstraction using Rust paradigms.
