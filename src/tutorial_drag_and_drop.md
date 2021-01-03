### Drag and Drop

- [EventController](https://gtk-rs.org/docs/gtk/struct.EventController.html) — Self-contained handler of series of events
- [EventControllerKey](https://gtk-rs.org/docs/gtk/struct.EventControllerKey.html) — Event controller for key events
- [EventControllerScroll](https://gtk-rs.org/docs/gtk/struct.EventControllerScroll.html) — Event controller for scroll events
- [EventControllerMotion](https://gtk-rs.org/docs/gtk/struct.EventControllerMotion.html) — Event controller for motion events
- [Gesture](https://gtk-rs.org/docs/gtk/struct.Gesture.html) — Base class for gestures
- [GestureSingle](https://gtk-rs.org/docs/gtk/struct.GestureSingle.html) — Base class for mouse/single-touch gestures
- [GestureDrag](https://gtk-rs.org/docs/gtk/struct.GestureDrag.html) — Drag gesture
- [GestureLongPress](https://gtk-rs.org/docs/gtk/struct.GestureLongPress.html) — "Press and Hold" gesture
- [GestureMultiPress](https://gtk-rs.org/docs/gtk/struct.GestureMultiPress.html) — Multipress gesture
- [GesturePan](https://gtk-rs.org/docs/gtk/struct.GesturePan.html) — Pan gesture
- [GestureSwipe](https://gtk-rs.org/docs/gtk/struct.GestureSwipe.html) — Swipe gesture
- [GestureRotate](https://gtk-rs.org/docs/gtk/struct.GestureRotate.html) — Rotate gesture
- [GestureZoom](https://gtk-rs.org/docs/gtk/struct.GestureZoom.html) — Zoom gesture
- [GestureStylus](https://gtk-rs.org/docs/gtk/struct.GestureStylus.html) — Gesture for stylus input
- [PadController](https://gtk-rs.org/docs/gtk/struct.PadController.html) — Controller for drawing tablet pads

- Tutorial [drag_and_drop.rs](drag_and_drop.rs)

Setting up drag and drop between widgets consists of selecting a drag source (the widget which the user starts the drag from) with the Gtk.Widget.drag_source_set() method, selecting a drag destination (the widget which the user drops onto) with the Gtk.Widget.drag_dest_set() method and then handling the relevant signals on both widgets.

Instead of using Gtk.Widget.drag_source_set() and Gtk.Widget.drag_dest_set() some specialised widgets require the use of specific functions (such as Gtk.TreeView and Gtk.IconView).

A basic drag and drop only requires the source to connect to the “drag-data-get” signal and the destination to connect to the “drag-data-received” signal. More complex things such as specific drop areas and custom drag icons will require you to connect to additional signals and interact with the Gdk.DragContext object it supplies.

In order to transfer data between the source and destination, you must interact with the Gtk.SelectionData variable supplied in the “drag-data-get” and “drag-data-received” signals using the Gtk.SelectionData get and set methods.
21.1. Target Entries

To allow the drag source and destination to know what data they are receiving and sending, a common list of Gtk.TargetEntry's are required. A Gtk.TargetEntry describes a piece of data that will be sent by the drag source and received by the drag destination.

There are two ways of adding Gtk.TargetEntry's to a source and destination. If the drag and drop is simple and each target entry is of a different type, you can use the group of methods mentioned here.

If you require more than one type of data or wish to do more complex things with the data, you will need to create the Gtk.TargetEntry's using the Gtk.TargetEntry.new() method.
21.2. Drag Source Signals

Name


When it is emitted


Common Purpose

drag-begin


User starts a drag


Set-up drag icon

drag-data-get


When drag data is requested by the destination


Transfer drag data from source to destination

drag-data-delete


When a drag with the action Gdk.DragAction.MOVE is completed


Delete data from the source to complete the ‘move’

drag-end


When the drag is complete


Undo anything done in drag-begin
21.3. Drag Destination Signals

Name


When it is emitted


Common Purpose

drag-motion


Drag icon moves over a drop area


Allow only certain areas to be dropped onto

drag-drop


Icon is dropped onto a drag area


Allow only certain areas to be dropped onto

drag-data-received


When drag data is received by the destination


Transfer drag data from source to destination
21.4. Example
_images/drag_and_drop_example.png

import gi
