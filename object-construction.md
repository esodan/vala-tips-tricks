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

In this case, `_index` is constructed at `GObjectClass` initialization, just one time for all your classes instantiation.



