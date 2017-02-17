# Introduction

Vala is not perfect. But who is these days?

You should use right tool for your problem. That's why there are lot of languages out there.

This chapter will explain you some existing limitations on Vala you should consider in order to deside if you are going to use it or fallback to C in a particular part of your software.

Vala relays on GObject, then its limitations are the ones for Vala too.

# Lambda parameters directions

While you can use a lambda method to attach to an object's signal, you can't use `out` type for a paramenter.

# Muti-Inheritance

GObject is designed to provide a C mechanism for inheritance, but based on C structs. This design makes impossible to have multi-inheritance  on GObject classes. The only way to have such a think is to implement interfaces with a set of virtual methods in place. For this reason there is no support for multi-inheritance in Vala.

