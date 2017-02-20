# GObject construction

Any Vala class deriving from `Object`, is constructed using C/GObject techniques. Take a tour on [GObject Initialization and Destruction](https://developer.gnome.org/gobject/stable/gtype-instantiable-classed.html#gtype-instantiable-classed-init-done) from API reference in order to better understand GObject process.

## Vala classes construction

In Vala, each time a class is instantiated `construct` block is executed.  if `Object.new (Typeof(YourClass))` is used, `construct` block is executed. If you don't define a constructor method, one is generated automatically for your object, then a `your_class_new` method is avairable as C API.

If you declare a variable and sets it to a value outside of `construct` block, then C generated code initialize your variables at object construction time by default.

```
public class YourClass : Object {
    private int _index = 0;
    public int index () { return i; }
}
```

Above code will initialize `_index` at construction time of `YourClass`, even if it is outside of `construct` block.

## GObjectClass initialization

In order initialize variables to be used by all your class instances, use `static` clause.

```
 public class YourClass : Object {
    private static int _index[] = {1, 2};
    public int index (int i) { return _index[i]; }
}
```

In this case, `_index` is set at `GObjectClass` initialization, just one time for all your each classes instantiation.

## this Variable

`this` variable is only available in instance methods or in construct blocks. In order to initialize a variable with reference to current instance you can use:

```
class Track : Object {
  public Evolution evolution = null;
  construct {
   evolution = new Evolution(this);
  }
}
class Evolution {
   private weak Track track;
   public Evolution(Track track) {
      this.track = track;
   }
}
```

# Object.new

`g_object_new()` method is used to create instances of GObject classes in C.

In Vala use Object.new, this allows you to:

* Initialize in one go all object properties, saving you a set of lines of code.
* Create objects of different types with common properties, like the ones implementing an interface

```
var obj = Object.new (typeof (MyClass), "property1", value1, "property2", value2, ...) as MyClass; 
```

If you have stored an object type to be used later, like when you use object collection of different types, you can use that to create object instances of required type.

```
var obj = Object.new (type_object, "property1", value1, ...);
```

In above example, you can't use obj as if it is of `type_object`, because you can't add code to cast at runtime, you  should know your object type. You may have an abstract parent class with methods implemented in `type_object` classes, you can use in your code to make some common tasks.

```
var obj = Object.new (type_object, "property1", value1, ...) as ParenClass;
message (obj.property1);
```



