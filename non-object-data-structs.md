# Structs

Structs in Vala are direct C structs. They need to be initialized using:

```
var v = Value ();
```

Here `GLib.Value` is a struct and is asigned to `v` allocating memory for all its members. It is a local variable. So if you need to modify outside its scope you should use `ref` keywork.

```
public struct Member {
  string name;
  int since;
}
public class ClassB : Object {
  public Member member { get; set; }
  public void initialize (ref Member mem) {
    mem.name = "Name";
    mem.since = 2017;
  }
  public static int main (string[] args) {
    var b = new ClassB ();
    var m = b.member; // Create a local copy of your struct
    b.initialize (ref m); // Pass a pointer to your local struct to modify
    b.member = m; // Copy back your struct to your property
    stdout.printf ("Member: %s - %d \n".printf (b.member.name, b.member.since));
    return 0;
  }
}
```

Vala advantage is to register your struct, so you can use in `Object` properties. It provides a set of methods like  copy and destroy, taking care about struct's members type, when possible in order to free or duplicate as necessary.

# 



