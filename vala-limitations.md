# Introduction

Vala is not perfect. But who is these days?

You should use right tool for your problem. That's why there are lot of languages out there.

This chapter will explain you some existing limitations on Vala you should consider in order to deside if you are going to use it or fallback to C in a particular part of your software.

Vala relays on GObject, then its limitations are the ones for Vala too.

# Lambda parameters directions

While you can use a lambda method to attach to an object's signal, you can't use `out` type for a paramenter.

# Muti-Inheritance

GObject is designed to provide a C mechanism for inheritance, but based on C structs. This design makes impossible to have multi-inheritance  on GObject classes. The only way to have such a think is to implement interfaces with a set of virtual methods in place. For this reason there is no support for multi-inheritance in Vala.

# Generics

When using Gee and Vala generics as properties, you should consider to initialize them first, both using a default or in construct block.

```
public class MyClass : Object {
    public ArrayList<Object> { get; set: default = new ArrayList<Object> (); }
}
```

Generics types are unknown at class initialization, but at instantiation time, then you should instantiate it and know generic type first.

This was done at GXml for SerializableArrayList&lt;G&gt;, where any object with this property type is initalized at declration using defaulto = new SerializableArrayList&lt;Object&gt;\(\); this avoids types unknowns.

In GXml Serializable, added an interface to declare it is a Collection Container then after create an object's instance using Object.new\(\), it calls a method implemented in interface to initialize all its generic property members.

