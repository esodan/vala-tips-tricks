# Vala C code generator

Vala provides `valac`, a tool to translate Vala code to C.

All C code uses GLib, GObject and GInterface, to provides Object Oriented Programming capabilites. If haven't that libraries yet, install them first.

All your generated code will follow [GObject Conventions](https://developer.gnome.org/gobject/stable/gtype-conventions.html), in order to provide consistent API between libraries using this GNOME technology. If you read them first, you can avoid common errors.

