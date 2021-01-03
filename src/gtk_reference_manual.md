### GTK+ Widgets and Objects (gtk-rs Reference)
1. Object Hierarchy
1. [Widget Gallery](https://developer.gnome.org/gtk3/stable/ch03.html)
1. Application support
   - [Application](https://gtk-rs.org/docs/gtk/struct.Application.html) — Application class
   - [ApplicationWindow](https://gtk-rs.org/docs/gtk/struct.ApplicationWindow.html) — GtkWindow subclass with GtkApplication support
   - [Actionable](https://gtk-rs.org/docs/gtk/struct.Actionable.html) — An interface for widgets that can be associated with actions
1. Interface builder
   - [Builder](https://gtk-rs.org/docs/gtk/struct.Builder.html) — Build an interface from an XML UI definition
   - [Buildable](https://gtk-rs.org/docs/gtk/struct.Buildable.html) — Interface for objects that can be built by GtkBuilder
1. Windows
   - [Window](https://gtk-rs.org/docs/gtk/struct.Window.html) — Toplevel which can contain other widgets
   - [Dialog](https://gtk-rs.org/docs/gtk/struct.Dialog.html) — Create popup windows
   - [MessageDialog](https://gtk-rs.org/docs/gtk/struct.MessageDialog.html) — A convenient message window
   - [AboutDialog](https://gtk-rs.org/docs/gtk/struct.AboutDialog.html) — Display information about an application
   - [Assistant](https://gtk-rs.org/docs/gtk/struct.Assistant.html) — A widget used to guide users through multi-step operations
   - [Invisible](https://gtk-rs.org/docs/gtk/struct.Invisible.html) — A widget which is not displayed
   - [OffscreenWindow](https://gtk-rs.org/docs/gtk/struct.OffscreenWindow.html) — A toplevel to manage offscreen rendering of child widgets
   - [WindowGroup](https://gtk-rs.org/docs/gtk/struct.WindowGroup.html) — Limit the effect of grabs
1. Layout Containers
   - [Box](https://gtk-rs.org/docs/gtk/struct.Box.html) — A container for packing widgets in a single row or column
   - [Grid](https://gtk-rs.org/docs/gtk/struct.Grid.html) — Pack widgets in rows and columns
   - [Revealer](https://gtk-rs.org/docs/gtk/struct.Revealer.html) — Hide and show with animation
   - [ListBox](https://gtk-rs.org/docs/gtk/struct.ListBox.html) — A list container
   - [FlowBox](https://gtk-rs.org/docs/gtk/struct.FlowBox.html) — A container that allows reflowing its children
   - [Stack](https://gtk-rs.org/docs/gtk/struct.Stack.html) — A stacking container
   - [StackSwitcher](https://gtk-rs.org/docs/gtk/struct.StackSwitcher.html) — A controller for GtkStack
   - [StackSidebar](https://gtk-rs.org/docs/gtk/struct.StackSidebar.html) — An automatic sidebar widget
   - [ActionBar](https://gtk-rs.org/docs/gtk/struct.ActionBar.html) — A full width bar for presenting contextual actions
   - [HeaderBar](https://gtk-rs.org/docs/gtk/struct.HeaderBar.html) — A box with a centered child
   - [Overlay](https://gtk-rs.org/docs/gtk/struct.Overlay.html) — A container which overlays widgets on top of each other [demo]
   - [ButtonBox](https://gtk-rs.org/docs/gtk/struct.ButtonBox.html) — A container for arranging buttons
   - [Paned](https://gtk-rs.org/docs/gtk/struct.Paned.html) — A widget with two adjustable panes
   - [Layout](https://gtk-rs.org/docs/gtk/struct.Layout.html) — Infinite scrollable area containing child widgets and/or custom drawing
   - [Notebook](https://gtk-rs.org/docs/gtk/struct.Notebook.html) — A tabbed notebook container
   - [Expander](https://gtk-rs.org/docs/gtk/struct.Expander.html) — A container which can hide its child
   - [Orientable](https://gtk-rs.org/docs/gtk/struct.Orientable.html) — An interface for flippable widgets
   - [AspectFrame](https://gtk-rs.org/docs/gtk/struct.AspectFrame.html) — A frame that constrains its child to a particular aspect ratio
   - [Fixed](https://gtk-rs.org/docs/gtk/struct.Fixed.html) — A container which allows you to position widgets at fixed coordinates
1. Display Widgets
   - [Label](https://gtk-rs.org/docs/gtk/struct.Label.html) — A widget that displays a small to medium amount of text
   - [Image](https://gtk-rs.org/docs/gtk/struct.Image.html) — A widget displaying an image
   - [Spinner](https://gtk-rs.org/docs/gtk/struct.Spinner.html) — Show a spinner animation
   - [InfoBar](https://gtk-rs.org/docs/gtk/struct.InfoBar.html) — Report important messages to the user
   - [ProgressBar](https://gtk-rs.org/docs/gtk/struct.ProgressBar.html) — A widget which indicates progress visually
   - [LevelBar](https://gtk-rs.org/docs/gtk/struct.LevelBar.html) — A bar that can used as a level indicator
   - [Statusbar](https://gtk-rs.org/docs/gtk/struct.Statusbar.html) — Report messages of minor importance to the user
   - [AccelLabel](https://gtk-rs.org/docs/gtk/struct.AccelLabel.html) — A label which displays an accelerator key on the right of the text
1. Buttons and Toggles
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
1. Numeric and Text Data Entry
   - [Entry](https://gtk-rs.org/docs/gtk/struct.Entry.html) — A single line text entry field
   - [EntryBuffer](https://gtk-rs.org/docs/gtk/struct.EntryBuffer.html) — Text buffer for GtkEntry
   - [EntryCompletion](https://gtk-rs.org/docs/gtk/struct.EntryCompletion.html) — Completion functionality for GtkEntry
   - [Scale](https://gtk-rs.org/docs/gtk/struct.Scale.html) — A slider widget for selecting a value from a range
   - [SpinButton](https://gtk-rs.org/docs/gtk/struct.SpinButton.html) — Retrieve an integer or floating-point number from the user
   - [SearchEntry](https://gtk-rs.org/docs/gtk/struct.SearchEntry.html) — An entry which shows a search icon
   - [SearchBar](https://gtk-rs.org/docs/gtk/struct.SearchBar.html) — A toolbar to integrate a search entry with
   - [Editable](https://gtk-rs.org/docs/gtk/struct.Editable.html) — Interface for text-editing widgets
1. Multiline Text Editor
   - Text Widget Overview — Overview of GtkTextBuffer, GtkTextView, and friends
   - [TextIter](https://gtk-rs.org/docs/gtk/struct.TextIter.html) — Text buffer iterator
   - [TextMark](https://gtk-rs.org/docs/gtk/struct.TextMark.html) — A position in the buffer preserved across buffer modifications
   - [TextBuffer](https://gtk-rs.org/docs/gtk/struct.TextBuffer.html) — Stores attributed text for display in a GtkTextView
   - [TextTag](https://gtk-rs.org/docs/gtk/struct.TextTag.html) — A tag that can be applied to text in a GtkTextBuffer
   - [TextTagTable](https://gtk-rs.org/docs/gtk/struct.TextTagTable.html) — Collection of tags that can be used together
   - [TextView](https://gtk-rs.org/docs/gtk/struct.TextView.html) — Widget that displays a GtkTextBuffer
1. Tree, List and Icon Grid Widgets
   - Tree and List Widget Overview — Overview of GtkTreeModel, GtkTreeView, and friends
   - [TreeModel](https://gtk-rs.org/docs/gtk/struct.TreeModel.html) — The tree interface used by GtkTreeView
   - [TreeSelection](https://gtk-rs.org/docs/gtk/struct.TreeSelection.html) — The selection object for GtkTreeView
   - [TreeViewColumn](https://gtk-rs.org/docs/gtk/struct.TreeViewColumn.html) — A visible column in a GtkTreeView widget
   - [TreeView](https://gtk-rs.org/docs/gtk/struct.TreeView.html) — A widget for displaying both trees and lists
   - [TreeView drag-and-drop](https://gtk-rs.org/docs/gtk/struct.FlowBox.html) — Interfaces for drag-and-drop support in GtkTreeView
   - [CellView](https://gtk-rs.org/docs/gtk/struct.CellView.html) — A widget displaying a single row of a GtkTreeModel
   - [IconView](https://gtk-rs.org/docs/gtk/struct.IconView.html) — A widget which displays a list of icons in a grid
   - [TreeSortable](https://gtk-rs.org/docs/gtk/struct.TreeSortable.html) — The interface for sortable models used by GtkTreeView
   - [TreeModelSort](https://gtk-rs.org/docs/gtk/struct.TreeModelSort.html) — A GtkTreeModel which makes an underlying tree model sortable
   - [TreeModelFilter](https://gtk-rs.org/docs/gtk/struct.TreeModelFilter.html) — A GtkTreeModel which hides parts of an underlying tree model
   - [CellLayout](https://gtk-rs.org/docs/gtk/struct.CellLayout.html) — An interface for packing cells
   - [CellArea](https://gtk-rs.org/docs/gtk/struct.CellArea.html) — An abstract class for laying out GtkCellRenderers
   - [CellAreaBox](https://gtk-rs.org/docs/gtk/struct.CellAreaBox.html) — A cell area that renders GtkCellRenderers into a row or a column
   - [CellAreaContext](https://gtk-rs.org/docs/gtk/struct.CellAreaContext.html) — Stores geometrical information for a series of rows in a GtkCellArea
   - [CellRenderer](https://gtk-rs.org/docs/gtk/struct.CellRenderer.html) — An object for rendering a single cell
   - [CellEditable](https://gtk-rs.org/docs/gtk/struct.CellEditable.html) — Interface for widgets that can be used for editing cells
   - [CellRendererAccel](https://gtk-rs.org/docs/gtk/struct.CellRendererAccel.html) — Renders a keyboard accelerator in a cell
   - [CellRendererCombo](https://gtk-rs.org/docs/gtk/struct.CellRendererCombo.html) — Renders a combobox in a cell
   - [CellRendererPixbuf](https://gtk-rs.org/docs/gtk/struct.CellRendererPixbuf.html) — Renders a pixbuf in a cell
   - [CellRendererProgress](https://gtk-rs.org/docs/gtk/struct.RendererProgress.html) — Renders numbers as progress bars
   - [CellRendererSpin](https://gtk-rs.org/docs/gtk/struct.RendererSpin.html) — Renders a spin button in a cell
   - [CellRendererText](https://gtk-rs.org/docs/gtk/struct.RendererText.html) — Renders text in a cell
   - [CellRendererToggle](https://gtk-rs.org/docs/gtk/struct.RendererToggle.html) — Renders a toggle button in a cell
   - [CellRendererSpinner](https://gtk-rs.org/docs/gtk/struct.RendererSpinner.html) — Renders a spinning animation in a cell
   - [ListStore](https://gtk-rs.org/docs/gtk/struct.ListStore.html) — A list-like data structure that can be used with the GtkTreeView
   - [TreeStore](https://gtk-rs.org/docs/gtk/struct.TreeStore.html) — A tree-like data structure that can be used with the GtkTreeView
1. Menus, Combo Box, Toolbar
   - [ComboBox](https://gtk-rs.org/docs/gtk/struct.ComboBox.html) — A widget used to choose from a list of items
   - [ComboBoxText](https://gtk-rs.org/docs/gtk/struct.ComboBoxText.html) — A simple, text-only combo box
   - [Menu](https://gtk-rs.org/docs/gtk/struct.Menu.html) — A menu widget
   - [MenuBar](https://gtk-rs.org/docs/gtk/struct.MenuBar.html) — A subclass of GtkMenuShell which holds GtkMenuItem widgets
   - [MenuItem](https://gtk-rs.org/docs/gtk/struct.MenuItem.html) — The widget used for item in menus
   - [RadioMenuItem](https://gtk-rs.org/docs/gtk/struct.RadioMenuItem.html) — A choice from multiple check menu items
   - [CheckMenuItem](https://gtk-rs.org/docs/gtk/struct.CheckMenuItem.html) — A menu item with a check box
   - [SeparatorMenuItem](https://gtk-rs.org/docs/gtk/struct.SeparatorMenuItem.html) — A separator used in menus
   - [ToolShell](https://gtk-rs.org/docs/gtk/struct.ToolShell.html) — Interface for containers containing GtkToolItem widgets
   - [Toolbar](https://gtk-rs.org/docs/gtk/struct.Toolbar.html) — Create bars of buttons and other widgets
   - [ToolItem](https://gtk-rs.org/docs/gtk/struct.ToolItem.html) — The base class of widgets that can be added to GtkToolShell
   - [ToolPalette](https://gtk-rs.org/docs/gtk/struct.ToolPalette.html) — A tool palette with categories
   - [ToolItemGroup](https://gtk-rs.org/docs/gtk/struct.ToolItemGroup.html) — A sub container used in a tool palette
   - [SeparatorToolItem](https://gtk-rs.org/docs/gtk/struct.SeparatorToolItem.html) — A toolbar item that separates groups of other toolbar items
   - [ToolButton](https://gtk-rs.org/docs/gtk/struct.ToolButton.html) — A GtkToolItem subclass that displays buttons
   - [MenuToolButton](https://gtk-rs.org/docs/gtk/struct.MenuToolButton.html) — A GtkToolItem containing a button with an additional dropdown menu
   - [ToggleToolButton](https://gtk-rs.org/docs/gtk/struct.ToggleToolButton.html) — A GtkToolItem containing a toggle button
   - [RadioToolButton](https://gtk-rs.org/docs/gtk/struct.RadioToolButton.html) — A toolbar item that contains a radio button
   - [Popover](https://gtk-rs.org/docs/gtk/struct.Popover.html) — Context dependent bubbles
   - [PopoverMenu](https://gtk-rs.org/docs/gtk/struct.PopoverMenu.html) — Popovers to use as menus
1. Selector Widgets and Dialogs
   - [ColorChooser](https://gtk-rs.org/docs/gtk/struct.ColorChooser.html) — Interface implemented by widgets for choosing colors
   - [ColorButton](https://gtk-rs.org/docs/gtk/struct.ColorButton.html) — A button to launch a color selection dialog
   - [ColorChooserWidget](https://gtk-rs.org/docs/gtk/struct.ColorChooserWidget.html) — A widget for choosing colors
   - [ColorChooserDialog](https://gtk-rs.org/docs/gtk/struct.ColorChooserDialog.html) — A dialog for choosing colors
   - [FileChooser](https://gtk-rs.org/docs/gtk/struct.FileChooser.html) — File chooser interface used by GtkFileChooserWidget and GtkFileChooserDialog
   - [FileChooserButton](https://gtk-rs.org/docs/gtk/struct.FileChooserButton.html) — A button to launch a file selection dialog
   - [FileChooserNative](https://gtk-rs.org/docs/gtk/struct.FileChooserNative.html) — A native file chooser dialog, suitable for “File/Open” or “File/Save” commands
   - [FileChooserDialog](https://gtk-rs.org/docs/gtk/struct.FileChooserDialog.html) — A file chooser dialog, suitable for “File/Open” or “File/Save” commands
   - [FileChooserWidget](https://gtk-rs.org/docs/gtk/struct.FileChooserWidget.html) — A file chooser widget
   - [FileFilter](https://gtk-rs.org/docs/gtk/struct.FileFilter.html) — A filter for selecting a file subset
   - [FontChooser](https://gtk-rs.org/docs/gtk/struct.FontChooser.html) — Interface implemented by widgets displaying fonts
   - [FontButton](https://gtk-rs.org/docs/gtk/struct.FontButton.html) — A button to launch a font chooser dialog
   - [FontChooserWidget](https://gtk-rs.org/docs/gtk/struct.FontChooserWidget.html) — A widget for selecting fonts
   - [FontChooserDialog](https://gtk-rs.org/docs/gtk/struct.FontChooserDialog.html) — A dialog for selecting fonts
   - [PlacesSidebar](https://gtk-rs.org/docs/gtk/struct.PlacesSidebar.html) — Sidebar that displays - frequently-used places in the file system
1. Oraments
   - [Frame](https://gtk-rs.org/docs/gtk/struct.Frame.html) — A bin with a decorative frame and optional label
   - [Separator](https://gtk-rs.org/docs/gtk/struct.Separator.html) — A separator widget
1. Scrolling
   - [Scrollbar](https://gtk-rs.org/docs/gtk/struct.Scrollbar.html) — A Scrollbar
   - [ScrolledWindow](https://gtk-rs.org/docs/gtk/struct.ScrolledWindow.html) — Adds scrollbars to its child widget
   - [Scrollable](https://gtk-rs.org/docs/gtk/struct.Scrollable.html) — An interface for scrollable widgets
1. Printing
   - [PrintOperation](https://gtk-rs.org/docs/gtk/struct.PrintOperation.html) — High-level Printing API [printing](printing.rs)
   - [PrintContext](https://gtk-rs.org/docs/gtk/struct.PrintContext.html) — Encapsulates context for drawing pages
   - [PrintSettings](https://gtk-rs.org/docs/gtk/struct.PrintSettings.html) — Stores print settings
   - [PageSetup](https://gtk-rs.org/docs/gtk/struct.PageSetup.html) — Stores page setup information
   - [PaperSize](https://gtk-rs.org/docs/gtk/struct.PaperSize.html) — Support for named paper sizes
   - [Printer](https://gtk-rs.org/docs/gtk/struct.Printer.html) — Represents a printer
   - [PrintJob](https://gtk-rs.org/docs/gtk/struct.PrintJob.html) — Represents a print job
   - [PrintUnixDialog](https://gtk-rs.org/docs/gtk/struct.PrintUnixDialog.html) — A print dialog
   - [PageSetupUnixDialog](https://gtk-rs.org/docs/gtk/struct.PageSetupUnixDialog.html) — A page setup dialog
1. Shortcuts Overview
   - [ShortcutsWindow](https://gtk-rs.org/docs/gtk/struct.ShortcutsWindow.html) — Toplevel which shows help for shortcuts
   - [ShortcutsSection](https://gtk-rs.org/docs/gtk/struct.ShortcutsSection.html) — Represents an application mode in a GtkShortcutsWindow
   - [ShortcutsGroup](https://gtk-rs.org/docs/gtk/struct.ShortcutsGroup.html) — Represents a group of shortcuts in a GtkShortcutsWindow
   - [ShortcutsShortcut](https://gtk-rs.org/docs/gtk/struct.ShortcutsShortcut.html) — Represents a keyboard shortcut in a GtkShortcutsWindow
1. Miscellaneous
   - [Adjustment](https://gtk-rs.org/docs/gtk/struct.Adjustment.html) — A representation of an adjustable bounded value
   - [Calendar](https://gtk-rs.org/docs/gtk/struct.Calendar.html) — Displays a calendar and allows the user to select a date
   - [DrawingArea](https://gtk-rs.org/docs/gtk/struct.DrawingArea.html) — A widget for custom user interface elements
   - [GLArea](https://gtk-rs.org/docs/gtk/struct.GLArea.html) — A widget for custom drawing with OpenGL
   - [EventBox](https://gtk-rs.org/docs/gtk/struct.EventBox.html) — A widget used to catch events for widgets which do not have their own window
   - [HandleBox](https://gtk-rs.org/docs/gtk/struct.HandleBox.html) — a widget for detachable window portions
   - [IMContextSimple](https://gtk-rs.org/docs/gtk/struct.IMContextSimple.html) — An input method context supporting table-based input methods
   - [IMMulticontext](https://gtk-rs.org/docs/gtk/struct.IMMulticontext.html) — An input method context supporting multiple, loadable input methods
   - [SizeGroup](https://gtk-rs.org/docs/gtk/struct.SizeGroup.html) — Grouping widgets so they request the same size
   - [Tooltip](https://gtk-rs.org/docs/gtk/struct.Tooltip.html) — Add tips to your widgets
   - [Viewport](https://gtk-rs.org/docs/gtk/struct.Viewport.html) — An adapter which makes widgets scrollable
   - [Accessible](https://gtk-rs.org/docs/gtk/struct.Accessible.html) — Accessibility support for widgets [accessibility demo](accessibility.rs)
1. Abstract Base Classes
   - [GtkWidget](https://gtk-rs.org/docs/gtk/struct.Widget.html) — Base class for all widgets
   - [GtkContainer](https://gtk-rs.org/docs/gtk/struct.Container.html) — Base class for widgets which contain other widgets
   - [GtkBin](https://gtk-rs.org/docs/gtk/struct.Bin.html) — A container with just one child
   - [GtkMenuShell](https://gtk-rs.org/docs/gtk/struct.MenuShell.html) — A base class for menu objects
   - [GtkRange](https://gtk-rs.org/docs/gtk/struct.Range.html) — Base class for widgets which visualize an adjustment
   - [GtkIMContext](https://gtk-rs.org/docs/gtk/struct.IMContext.html) — Base class for input method contexts
   - [GtkNativeDialog](https://gtk-rs.org/docs/gtk/struct.NativeDialog.html) — Integrate with native dialogs
1. Cross-process Embedding
   - [GtkPlug](https://gtk-rs.org/docs/gtk/struct.Plug.html) — Toplevel for embedding into other processes
   - [GtkSocket](https://gtk-rs.org/docs/gtk/struct.Socket.html) — Container for widgets from other processes
1. Recently Used Documents
   - [RecentManager](https://gtk-rs.org/docs/gtk/struct.RecentManager.html) — Managing recently used files
   - [RecentChooser](https://gtk-rs.org/docs/gtk/struct.RecentChooser.html) — Interface implemented by widgets displaying recently used files
   - [RecentChooserDialog](https://gtk-rs.org/docs/gtk/struct.RecentChooserDialog.html) — Displays recently used files in a dialog
   - [RecentChooserMenu](https://gtk-rs.org/docs/gtk/struct.RecentChooserMenu.html) — Displays recently used files in a menu
   - [RecentChooserWidget](https://gtk-rs.org/docs/gtk/struct.RecentChooserWidget.html) — Displays recently used files
   - [RecentFilter](https://gtk-rs.org/docs/gtk/struct.RecentFilter.html) — A filter for selecting a subset of recently used files
1. Choosing from installed applications
   - [AppChooser](https://gtk-rs.org/docs/gtk/struct.AppChooser.html) — Interface implemented by widgets for choosing an application
   - [AppChooserButton](https://gtk-rs.org/docs/gtk/struct.AppChooserButton.html) — A button to launch an application chooser dialog
   - [AppChooserDialog](https://gtk-rs.org/docs/gtk/struct.AppChooserDialog.html) — An application chooser dialog
   - [AppChooserWidget](https://gtk-rs.org/docs/gtk/struct.AppChooserWidget.html) — Application chooser widget that can be embedded in other widgets
1. Gestures and event handling
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

### GTK+ Core Reference
   - Main loop and Events — Library initialization, main event loop, and events
   - Version Information — Variables and functions to check the GTK+ version
   - [Accelerator Groups](https://gtk-rs.org/docs/gtk/struct.AccelGroup.html) — Groups of global keyboard accelerators for an entire GtkWindow
   - [Accelerator Maps](https://gtk-rs.org/docs/gtk_sys/struct.AccelMap.html) — Loadable keyboard accelerator specifications
   - [Clipboards](https://gtk-rs.org/docs/gtk/struct.Clipboard.html) — Storing data on clipboards
   - Drag and Drop — Functions for controlling drag and drop handling [refer WidgetExt](WidgetExt)
   - [Settings](https://gtk-rs.org/docs/gtk/struct.Settings.html) — Sharing settings between applications
   - Bindings — Key bindings for individual widgets [refer BingdingEntry](gtk_sys/GtkBindingEntry)
   - Standard Enumerations — Public enumerated types used throughout GTK+
   - Selections — Functions for handling inter-process communication via selections [refer SelectionData](https://gtk-rs.org/docs/gtk/struct.SelectionData.html)
   - Testing — Utilities for testing GTK+ applications
   - Filesystem utilities — Functions for working with GIO
