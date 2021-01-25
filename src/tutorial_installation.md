## Installation

- [Rust and Gtk-rs](https://gtk-rs.org/docs-src/tutorial/rust_and_gtk)
- [Gnome libraries and Rust](https://gtk-rs.org/docs-src/tutorial/gnome_and_rust)

### Rust and Gtk-rs

Before going any further, if you don’t know Rust at all, we recommend you to read the official Rust Book.
Then we recommend you to learn a bit about Cargo and check the GTK requirements.

All done? Perfect!

#### Adding Gtk-rs as dependency

Let’s start with the basics. I assume you already created a project with a Cargo.toml file in it. To add the Gtk-rs’ gtk crate as dependency, it’s as simple as follow:
``` rust
[dependencies]
gtk = "0.1.0"

Then from your “main” file (understand the entry point of your program/library), add:

extern crate gtk;

Of course, the same goes for any other Gtk-rs crate. Example with glib:

[dependencies]
glib = "0.1.0"
```

And:
``` rust
extern crate glib;
```

### Get last version

If a new Gtk-rs release happens, just go to crates.io and check for the Gtk-rs crates version you’re using. Update the version to your Cargo.toml file:
``` rust
gtk = "0.2.0"
```
Then just compile normally, cargo will update the dependency by itself.

### Examples

Now that you know how to import Gtk-rs crates into your code, looking at the examples repository could be a great idea!
