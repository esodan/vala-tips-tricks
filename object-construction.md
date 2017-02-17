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

## GType and GObjectClass

In order to have a `GObjectClass` initialized before any class is instantiated, you should use \([Bug \#543189](https://bugzilla.gnome.org/show_bug.cgi?id=543189)\):

```
typeof(MyType).class_ref();
```

`class_ref()` method instructs `GObjectt`type system to initialize its `GObjecClass`.

## Type Registration

Once an object is created it is registered in `GObject` type system, allowing you to use `object is YourBaseObject` . If you try to use a type without registration will above sentences will always fail at runtime. Use `typeof(YourBaseObject)` in order to register your type.

This is a problem for libraries, because they couldn't have all your types initialized before its use. Make shure to call an initialization method at each entry point of your library.

# this Variable

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



