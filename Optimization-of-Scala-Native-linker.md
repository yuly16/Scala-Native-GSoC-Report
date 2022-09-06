# Optimization of Scala Native linker

## 1. Introduction

Scala Native is an optimizing ahead-of-time compiler for scala. Traditional scala code is compiled to jvm-interpretable bytecode, while Scala Native directly compiles scala code to binaries. Here are two main steps in Scala Native to compile the scala code to binaries: first the scala code is compiled to `nir` by NIR compiler; second `nir` code is loaded, optimized and transformed to `llvm-ir` code by Scala Native Linker. During the GSoC period, my task is to investigate how to speed up Scala Native Linker. Here are four products in my project: 

* Build benchmarks for evaluating the performance of Scala Native, and automatic test script to measure the compilation and and runtime performance

* Introduce incremental compilation to Scala Native, which reduces the build time by 21% on average. 

* Profile the optimizer of Scala Native. Based on the profile result, we decrease the memory cost and fix the issue that Scala Native is stuck when compiling very large projects on release mode.

* Investigate the feasibility of parallel optimization. The conclusion is that parallel optimization is nontrivial to implement in the current Scala Native optimizer. Finally we will give some possible solutions to do parallel optimization in the future.

# 2. Scala Native Benchmark Evaluation

[Scala Native Autotest](https://github.com/yuly16/incremental-compilation-autotest) is the tool we created to automatically test the performance of Scala Native. The usage of the script is:

```
./autotest --scala SCALA-VERSION --scala-native SCALA-NATIVE-VERSION --benchmark-list <benchmarks list or non to run all>
```

And then the compilation and runtime time cost are collected in a csv file, which makes it easier to analyze our changes to Scala Native. 

The scala code benchmark contains 18 scala projects refered from the [original Scala Native Benchmarks](https://github.com/scala-native/scala-native-benchmarks). We also write a `build.sbt` template. When the script is running, it will replace the placeholders in the template to the current Scala version, Scala Native version and benchmarks that need to test. The workflow of the autotest script is:

* 


* The scala code benchmark, which contains 18 scala projects. 

* The sbt `build.sbt` template.

* Linux shell workflow script

# 3. Incremental Compilation


benchmark we created to evaluate the compilation and runtime performance of Scala Native. This script 