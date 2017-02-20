# Structs

Structs in Vala are direct C structs. They need to be initialized using:

```
var v = Value ();
```

Here `GLib.Value` is a struct and is asigned to `v` allocating memory for all its members.
