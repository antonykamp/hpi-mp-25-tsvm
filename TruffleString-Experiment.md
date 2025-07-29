# TruffleString Experiment

> This document outlines the experiments conducted with the TruffleString class, including performance benchmarks, memory usage analysis, and other relevant findings.

## Introduction

### Background
<!-- How primitives and non primitives are represented -->
<!-- TruffleString class and its role in the Truffle framework -->

TruffleSqueak is a Squeak implementation on the GraalVM Truffle framework. It aims to leverage the performance and language interoperability benefits of Truffle while maintaining compatibility with Squeak's features.

This experiment focuses on the data representation of smalltalk objects in java. We differentiate between primitives (i.e. `ClassObject`) and non-primitives (i.e. `ByteString`, `ByteArray`, etc.). Primitive classes have a direct mapping to Java classes.

![Primitive Object Representation, Example: `ClassObject`](img/graal-fmc-primitive.drawio.png)

Non-primitive classes are represented by Java objects of the class `NativeObject` that encapsulate the data. Each `NativeObject` instance contains a `storage` and `class` object. The `storage` contains the actual data, while the `class` object provides metadata about the object type.

![Non-Primitive Object Representation, Example: `WideString`, `ByteArray`, `ByteString`](img/graal-fmc-nativeobject.drawio.png)

We want to investigate if we can improve the performance of string operations by leveraging tools provided by the Truffle framework.

### Baseline Performance
<!-- JSON Benchmark -->
<!-- Run on Antonys Computer -->
<!-- Results -->

To compare the performance of string operations, we decided to use the `JSON Benchmark` from the "Are We Fast Yet?" framework. We measure the time needed to parse 100 JSON strings and convert them into a Smalltalk object. We run the benchmark 300 times to ensure consistent results and to account for any warm-up effects.

The command to run the benchmark is as follows:

```bash
trufflesqueak --experimental-options --smalltalk.disable-startup --smalltalk.disable-interrupts --engine.Mode=default --engine.TraceCompilation --compiler.TracePerformanceWarnings=call,instanceof,store,trivial --engine.CompilationFailureAction=Print --engine.CompilationStatistics --log.file="./Json.trace.log" --quiet --code "AWFYHarness run: #('Json' 300 100)"
```

We run the benchmark on a machine with the following specifications:

- Apple MacBook Pro 2023
- Chip: Apple M3 Pro
- Memory: 16GB
- Operating System: macOS Sequoia 15.4.1

The results of the benchmark are as follows:

| Metric       | Baseline  |
| ------------ | --------- |
| Average Time | 201.466ms |
| Minimum Time | 173 ms    |
| Maximum Time | 1 532 ms  |
| Summary Time | 60 440 ms |

### Experiment Goals
<!-- Improved performance for string operations -->
<!-- Sideproduct: Improved interoperability with other languages -->

Truffle offers a specialized string class called `TruffleString`, designed to optimize string operations and enhance performance through vector representation and parallelism.

The goal is to explore how the Truffle framework can optimize string operations and improve performance by leveraging the capabilities of the `TruffleString` class.

We expect to achieve the following:

- Improved runtime performance for string operations.
- Enhanced interoperability with other languages supported by GraalVM.

## Experiment 1: Replace ByteStrings with TruffleString

### Implementation

<!-- Changed storage of ByteStrings to TruffleString -->

### Results

<!-- Performance decreased -->
<!-- Codesize increased -->
<!-- Compilation time and code size of string comparisons increased -->

### Discussion
<!-- Issue: Provide for each permutation of string types a separate method to avoid the overhead of type checks -->
<!-- Reduce permutation by replacing ByteArrays with TruffleString -->

## Experiment 2: Replace ByteArray with TruffleString

### Implementation

<!-- Changed storage of ByteArray to TruffleString -->

### Results

<!-- Performance improved to v1 -->
<!-- Codesize decreased to v1 -->

<!-- Performance decreased compared to original -->
<!-- Compilation time and code size of string comparisons decreased -->

### Discussion

<!-- Issue: Cannot use cool TruffleString features like substring, indexOf, etc. -->
<!-- Only use byte wise operations (read & write) because squeak does the operation by it self -->
<!-- Vector representation only make sense for big strings -->

<!-- Micro benchmark: -->
<!-- Improved performance for big strings -->

<!-- Idea: Would have to add (failing for OSVM) primitives to higher level functions to use the TruffleString features -->
<!-- Slow for OSVM -->

## Summary

<!-- Not fast now -->
<!-- TruffleString is optimized for big strings and big operations -->

## Future Work

<!-- Idea: Would have to add (failing for OSVM) primitives to higher level functions to use the TruffleString features -->