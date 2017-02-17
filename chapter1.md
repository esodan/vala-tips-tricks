# Vala C code generator

Vala provides `valac`, a tool to translate Vala code to C.

All C code uses GLib, GObject and GInterface, to provides Object Oriented Programming capabilites. If haven't that libraries yet, install them first.

All your generated code will follow [GObject Conventions](https://developer.gnome.org/gobject/stable/gtype-conventions.html), in order to provide consistent API between libraries using this GNOME technology. If you read them first, you can avoid common errors.

valac just produce valid C code if you follow a [GObject Conventions](https://developer.gnome.org/gobject/stable/gtype-conventions.html) and take in account the ones described in this chapter.

# Class Names

All your classes's name should use `CamelCase` convention. Don't use underscope `_` , they are used to separate methods names.

## Interfaces Names

Use same conventions as instantiable classes, because they at the end are types and classes, but un-instantiable.

# Namespaces

All your classes should be in a namespace both using `namespace` clause or prefixing your class name at declaration time.

```
public Prx.YourClass : Object {}
```

In above example, `YourClass` is a class name with a prefix `Prx`. In C it will use `PrxYourClass` as type name.

If you generate code without namespaces, is possible to produce invalid C code without notice.

# Class Methods

All methods declared as part of a class declaration, are prefixed using lower case name of class and `_` as a separator.

```
public Prx.YourClass : Object {
    public void method () {}
}
```

`method` as a C code will be: `prx_yourclass_method`.

Large methods names should use `_` as separators, avoid `CamelCase` syntax, because its against **GObject** method conventions.

```
public Prx.YourClass : Object {
    public void method_name () {}
}
```

`method_name`_as a C code will be: _`prx_your_class_method_name`.

