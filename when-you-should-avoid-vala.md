# Vala usefulness

If you write GLib/GObject based software, Vala provides a very convenient and product syntax to produce C code. Special mention about libraries using GObject is they are easily bindable through GObject Introspection.

Few lines of code in Vala can save you lot of lines in C, even if you use macros.

Object Oriented Programming is easiest in Vala than in C. Its syntax makes easy to think Object Oriented, which is hard if you  are using C, but possible of course, because at the end Vala produce C code.

Subclassing existing classes like create a new GTK+ widget, are easy and with few lines of code.

# C Generated Code

Vala compiler, is a C generator code, for GObject based software. But C flexibility and possibilities is hard to reproduce, some times because some of C syntax can be against Object Oriented recommendations practices.

If you are working on Object Oriented Flow to produce C code, use Vala.

If you need grained control on structs and avoid limitations imposed by Vala, like specific field types in interfaces, you should write your class or interface using pure C and GObject.

Is important to follow [GObject Introspection recommendations](https://wiki.gnome.org/Projects/GObjectIntrospection/WritingBindingableAPIs) about your C API in order to make easy to be bindable. This will help to write Vala bindings more easily too.

Vala generated code is not optimized to be read by humans, still easy to follow if you need it, C code inspection are not necesary for Vala programmers at every compilation.

# GLib Contribution

Consider to write your pice of code in C if you plan to backport to GLib or GObject, because Vala generated code have been designed to be easily produced not readed.



