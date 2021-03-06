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

# Class Properties

Class or interface properties should use lowercase names. Long names should use `_` as word separator.

```
public class Exm.Letter {
    public string name { get; set; }
    public int vertical_size { get; set; }
}
```

Properties's accessors in C for above methods are `exm_letter_get_name()` and exm\_letter\_get\_vertical\_size\(\), this is why you can't use `type` as a property name; it will be mapped to `exm_letter_get_type()`, according with GObject C coding conventions it should be used to register and return object's type and Vala create one for your class automatically; at the end you'll have two methods of the same name at C compilation time.

# var keyword

`var` keyword is a short way to declare new variables and should be used on typed declaration: a typed return value from a method, a variable or constant. Typed variables shoud be used in Vala and is recommended, but valid, to declare a variable as `var l = null` this declaration use `gpointer` as variable type, in Vala may have no sense but in C.

