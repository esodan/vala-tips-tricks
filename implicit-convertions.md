# Constants

There are some implicit conversions of constants. Programmers should take care about them in order to avoid miss behavior of  code at running time.

```
uint i = -1;
```

In above example unsigned integer is set to negative value, but it just convert it to unsigned, then asigned value will be, in some systems, `4294967295` instead.

