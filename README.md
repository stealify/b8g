# b8g
A V8 distribution written in Stealify Language designed to get used as ring 0 

## What?
This is a v8 Fork designed to get used as OS Kernel Replacement implementing a Capability Module Based Universal ABI.
That sounds Technical?

It is a POSIX Nix like Kernel Implementing a nixOs Like Environment based on the Stealify Lang which is a Restricted Super Set Of ECMAScript that can be transpiled into both directions. It is designed to get used as Top Level IDL so called Glue Code for Modules and Components. It Already is widly known as Javascript for historical reason but we avoid that name and refer to Stealify Lang which is in General Compatible to ECMAScript / Typescript / v8 Torque or Kotlin.

b8g compiles so called snapshots they are something like a container image but in a more raw nativ format 

src/snapshot/snapshot.cc
```
  // Snapshot blob layout:
  // [0] number of contexts N
  // [1] rehashability
  // [2] checksum
  // [3] (128 bytes) version string
  // [4] offset to readonly
  // [5] offset to context 0
  // [6] offset to context 1
  // ...
  // ... offset to context N - 1
  // ... startup snapshot data
  // ... read-only snapshot data
  // ... context 0 snapshot data
  // ... context 1 snapshot data
```
