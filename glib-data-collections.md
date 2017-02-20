# GLib.List&lt;G&gt;

If you check at `GList`, it hasn't a `GDestroyNotify` at initialization, like `GHashTable`, no `g_list_remove()` returns data to handle by Vala automatically, then is your responsability as a programmer to know how to handle data, in this case each time you call `GLib.List.remove()` on ref counted objects, you should decrease it by calling `unref() `explicitly in Object classes or the one provided by your bindings.

So if GLib adds a new `GLib.List<Object>()` specialized handler for `GObject` classes, taking care about ref/unref, we just take care on using `GLib.List<G> `on Objects and use `Gee.ArrayList<G>` instead.

Use `GLib.List<G>` as returning value where your class takes care about your objects not returned GLib.List&lt;G&gt; one.

If you create a `GLib.List<G>` as return value, creating one using `append()`, as described, advice your user to `unref()` all returned objects using `GLib.List<G>.foreach()` before get out of context.

For public API you may want to use `GLib.Queue()` instead, it returns removed objects, then it can be `unref()` by Vala automatically.



