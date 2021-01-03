### Clipboard

Gtk.Clipboard provides a storage area for a variety of data, including text and images. Using a clipboard allows this data to be shared between applications through actions such as copying, cutting, and pasting. These actions are usually done in three ways: using keyboard shortcuts, using a Gtk.MenuItem, and connecting the functions to Gtk.Button widgets.

There are multiple clipboard selections for different purposes. In most circumstances, the selection named CLIPBOARD is used for everyday copying and pasting. PRIMARY is another common selection which stores text selected by the user with the cursor.
