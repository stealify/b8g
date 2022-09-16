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

a context is a data structure representing the JS Representation including the links and function calls to the Components often referenced as Modules while you can see there is no concept of Dynamic Modules inside a JS Engine this is a Concept of JS Runtimes b8g does not Implement a Runtime it is runtime and engine agnostic tooling written in ECMAScript using its own Concepts while there will exist a b8g-runtime at some point we do as of current time of writing this refer always to justjs as the proof of concept it is linux only at present but it implements a good starting point alternatives would be graalvm, or deno v8 bindings. see: 
- [ ] - https://github.com/denoland/deno/issues/1877

