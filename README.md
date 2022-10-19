# b8g (Big Engine) 
The Core of b8g is the universal module or lets better say component system it combines a complet vm build kit. It offers only the bare minimum needed for that. Every Stealify Project runs on this engine it is the raw core of most stealify fundamentals.

This level of Granularity is the solution to all development problems in the future. Its main aim is to Replace LLVM at some Point and even Integrate all gcc features optional this solves the long discussion about licences as we all know Stealifys main goal is making all under The Unlicense and Stealify Lang as a Meta Language Unlicenses all Other Languages because no one can license or patent or license Generic Arithmetic which is a Math concept. So do not get confused we take care of the rest.

every component accepts sharedMemory as also none shared one and a additional callback. thats it also even function parameters or eveything else needed is supplyed via shared memory as transport there is no concept of std input output a component is a composition of Functional Streams that operate on Handels a handel can represent diffrent backends like sharedMemory or a file the handle is the Interface for the Software while you can use inside the handle implementation other low level primitives but you should always reuse as much existing components as possible as this will lead to better faster code as every code is isolated by design there is never sharedState between components only if a component passes its handels to a other component so you are fully aware what shares state.

the above described concepts allow us to partial incremental stealify every existing software or even every software that will ever get written into this Stealify Project which creates then a big repo of Unlicensed Components that you can use without headache. 

## Security Model
a context is isolated and has no access to other contexts but they also got a secret key a symbol that you can use to link them up.


## Features 
- Operate on SharedMemory
- Capability based Component Model
- Implements Tasks, Streams, Events, as also stdio, fd for backward compat with legacy apps
- directly address and executable binary serialised stack format that is easy to understand and execute without much additional tooling. allows to expose components of the stack via capability based protocol so isolation and security build in by design.

## Fundamental Concepts
Stack is a Reference able composition of binary instructions that are executeable. This abstraction level allows us to run anywhere. 

### module / component 
Both mean the same both end up on the stack while the loading function can be diffrent our final goal is to get everything into the component state as much as possible. So we can focus on fundamentals like calling conventions in assembly and code optimization.

### snapshot
a binary serialisation of a dynamic execution context also often named state for example tar is a snapshot format for files it serialises them into a single binary representation that is later deserialise able fast doing that with something that dynamicly changes is called a snapshot. A screenshoot for example is also a Snapshot where image is the format. We Serialise into offset addressed Stack Images in our current implementation. This allows us to work with raw binary data without the need to assign it to a symbol like we would need to do in a shared object in c.

### Universal Compiler Feedback Interface for LLVM/GCC/V8/GRAALVM
A Compiler Feedback Interface tooling for Runtimes mainly used to build a StealifyVM distribution written in Stealify Language designed to get used as ring 0 with or without a Linux Kernel offers Adapters for *Nix Kernel and InitD Replacements like SysV SystemD. It is able to take Snapshots that can directly get used in Diffrent Runtime Environments or Standalone.

This Project is a dependencie of, 
- @stealify/compiler
- @stealify/v8/lib/snapshots
- @stealify/v8/lib/justjs
- @stealify/v8/lib/justjs-smol

## What?
implementing a Capability Module Based Universal ABI to build Apps and Software Stacks that run without additional overhead directly Isolated and Secure
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

a context is a data structure representing the JS/ECMAScript v8 raw Representation including the links and function calls to the Components often referenced as Modules while you can see there is no concept of Dynamic Modules inside a Engine this is a Concept of Runtimes b8g does not Implement a Runtime it is runtime and engine agnostic tooling written in ECMAScript/Stealify Lang using its own Concepts while there will exist a b8g-runtime at some point we do as of current time of writing this refer always to justjs as the proof of concept it is linux only at present but it implements a good starting point alternatives would be graalvm, or deno v8 bindings. see: 
- [ ] - https://github.com/denoland/deno/issues/1877

b8g is mostly compare able to the graal jvmci and lvvm gcc in fact b8g also implements the jvmci and can fully interop with it also via our LLVM/GRAALVM integrations as also its own Java Bytecode Frontend.

In Fact b8g can be used as native-image replacement target you can see b8g also as replacement for the following engines: docker, libcontainer, kubernetes, mesos, linux, v8, JVM, GraalVM, LLVM, GCC, Zircon (FuchsiaOS), Android, and many more. 

## Diffrence between hardware VM's and b8g
b8g is it self designed as hypervisor and hypervisor monitor as also manager it offers its own components it does not need the concepts of hardware virtualisation as it does not implements the concept of hardware at all it implements 1 single concept called the component concept that includes hardware so hardware access is always via b8g offerd api's possible in a unified isolated secure way by design no abstraction like a hardware vm is needed to archive all design goals that hardware virtual machines to do implement and offer. For backward compatability it offers components that emulate popular hypervisors or even runs them directly. b8g is designed to run even at ring 0 hardware level it is a low level implementation designed to implement the stealify language.

## Examples
- [ ] Using justjs static build.
- [ ] Using quarkus + es4x (graaljs) + graalvm native image as target.
- [ ] expose the justjs c++ api as external c to deno to enable a single shared code base for the snapshot tooling. 

## What makes b8g diffrent to raw v8
It exposes additional api's and interfaces as also integrations for Low Level Code Compilers like GraalVM and LLVM or GCC while it offers a universal Compiler Feedback Interface and the needed tools to integrate new Compilers. In general it is the core component of Stealify's Polyglot Muli Pass Compiler and AI Tooling. It Reuses only Concepts of V8 and will not share the Implementation Details. We Incremental Recode v8 in Stealify Lang via b8g.
So depending on v8 is a temporary Factor but staying Compatible with v8 will be always the case b8g will always produce v8 compatible snapshots and will also add stable abi's to that.

## What is this used for explained as use case
Together with some other Components of the Stealify Stack this is used to:
- Replace Linux Container Concepts with Unikernels (Docker)
- Deploy Secure VM's
- Deploy and Orgistrate Whole Cloud Provider Deployments at Exabyte Scale with confidence! Fully Declarativ Isolated Secure. 
- use it as Kubernets Replacement
- use it as Linux Replacement
- use it as WASI WASM Replacement
