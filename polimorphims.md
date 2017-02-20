# Polimorphim

You can use GObject to create new specialiced classes. Its design doesn't allow polimorphim.

GInterface allows to your classes to be used as if they are of different type. This is GObject/GInterface to provide polimorphim.

# Deriving classes

It is recommended you learn how to derive C classes, got to [GObject Reference](https://developer.gnome.org/gobject/stable/chapter-gobject.html) for a detailed explanation. All boiler plate in C is simplified in Vala.

```
public class Base : Object {
    public string name { get; set; }
}
```

`Base` is a `GObject` class deriving from `Object` \(`GObject` in C\). This class defines a new property `name`.

## Abstract classes

Abstract classes can have both properties or methods to be implemented by derived classes. Is an error to declare abstract a class without any abstract method or properties.

```
/* Don't do this please */
public abstract class Base : Object {
    public string key { get; set; }
}
```

## base keyword

`base` keyword shoud be used to access methods or properties you have overrided in derived classes. If you do so on non virtual methods or properties, can produce invalid C code from Vala Code Generator.

## Derived class's properties

Is not recommended to declare a property with same type and name of base class, because you can use your base class's property as if it was defined in your derived class.

Declaring a property with same type and name, using `new` keyword, and then use `base` keyword to access base class is a programming error and confuse Vala Code Generator.

```
class Base : Object {
        public int index { get; set; default = 1; }
}

class Derived : Base {
        public new int index { set; get; default = 3; }
}

void main () {
        var obj = new Derived ();
        message ("Prop: "+obj.index.to_string ());
}
```

In this example `Derived` class use its index property and avoids any value defined in base class.

# GObject Type System

GObject provides a runtime type system to identify different properties. Because is runtime, you can't assume its value at any time and will change next execution. See [GObject Documentation](https://developer.gnome.org/gobject/stable/gobject-Type-Information.html) to learn more about.

A type should be registered before to use it. By knowing its value you can know if it is fundamental or derived from other, like a subclass or implementing an interface.

When you instantiate a class, GObject register it in type system, then you can use it. Abstract classes and interfaces are registered when its `*get_type()` is used.

## Initialize Type without instantiate

In order to have a`GObjectClass`initialized before any class is instantiated, you should use \([Bug \#543189](#)\):

```
typeof(MyType).class_ref();
```

`class_ref()`method instructs`GObject`type system to initialize its`GObjecClass`.

