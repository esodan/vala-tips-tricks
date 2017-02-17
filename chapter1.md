# Vala C code generator

Vala provides `valac`, a tool to translate Vala code to C.

All C code uses GLib, GObject and GInterface, to provides Object Oriented Programming capabilites. If haven't that libraries yet, install them first.

All your generated code will follow [GObject Conventions](https://developer.gnome.org/gobject/stable/gtype-conventions.html), in order to provide consistent API between libraries using this GNOME technology. If you read them first, you can avoid common errors.

## Class Names

All your classes shoule use `CamelCase` convention.

## Namespaces

All your classes should be in a namespace both using `namespace` clause or prefixing your class name at declaration time.

```vala
public Prx.YourClass : Object {}
```

In above example, `YourClass` is a class name with a prefix `Prx`. In C it will use `PrxYourClass` as type name.



