# eJSTK

eJSTK is a toolkit to develop a subset of JavaScript VM.

## Publication

Takafumi Kataoka, Tomoharu Ugawa, Hideya Iwasaki:
A Framework for Constructing JavaScript Virtual Machines with Customized Datatype Representations,
ACM SAC 2018.

## Contents

This repository contains three submodules for tools developed in the eJS project.
  * `ejsvm`  --- eJSVM compiler
  * `vmgen`  --- tools for generating datatype part and instruction part of the eJSVM
  * `ejsc`  --- JavaScript compiler to eJSVM code

## Quick Start

Please note that eJSVM currently supports only a subset of JavaScript.
If your JavaScript program does not work, please try a simpler example.

### Prepare source files

 1. Clone all submodules

 2. Make symbolic link to vmgen under ejsvm
 ```
 cd ejsvm
 ln -s ../vmgen
 ```

### eJS Compiler

 1. Download the following files and place them under `ejsc/libs`.

   * antlr-4.5.3-complete.jar
   * javax.json-1.0.4.jar

 2. Build by `make compiler.jar` under `ejsc` directory.

 3. `compiler.jar` will be created.  Execute it.  Following command
    will compile a JavaScript file `sample.js` and create `sample.sbc`.

 ```
 $ java -jar compiler.jar sample.js
 ```

### eJSVM

 1. Build vmgen by `ant` under the `ejsvm/vmgen` directory.

 2. Create the common part of Makefile `ejsvm/common.mk`.
    `ejsvm/common.mk.template` is the template.  You may need to
    modify it for your environment.

 3. Create a build directory.  For example, `mkdir ejsvm/build`.

 4. Create a `Makefile` under the build directory.  `Makefile` specifies a datatype definition file and a operand specification file, and includes `common.mk`. The following example is a Makefile for a VM with default type definitions and instructions accepting any datatype of operands.

 ```
 .PRECIOUS: %.c %.h
 DATATYPES=../datatypes/default.def
 OPERANDSPEC=../operand-spec/any.spec
 CFLAGS=-DNDEBUG -UDEBUG -O3
 include ../common.mk

 ```

 5. Build by `make`.

 6. Execute an sbc file by `./ejsvm sample.sbc` execute `sample.sbc`.
