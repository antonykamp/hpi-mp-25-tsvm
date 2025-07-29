# TruffleString Experiment

> This document outlines the experiments conducted with the TruffleString class, including performance benchmarks, memory usage analysis, and other relevant findings.

## Introduction

### Background
<!-- How primitives and non primitives are represented -->
<!-- TruffleString class and its role in the Truffle framework -->

TruffleSqueak is a Squeak implementation on the GraalVM Truffle framework. It aims to leverage the performance and language interoperability benefits of Truffle while maintaining compatibility with Squeak's features.

This experiment focuses on the data representation of smalltalk objects in java. We differentiate between primitives (i.e. `ClassObject`) and non-primitives (i.e. `ByteString`, `ByteArray`, etc.). Primitive classes have a direct mapping to Java classes.

![Primitive Object Representation, Example: `ClassObject`](img/graal-fmc-primitive.drawio.png)

Non-primitive classes are represented by Java objects of the class `NativeObject` that encapsulate the data. Each `NativeObject` instance contains a `storage` and `class` object. The `storage` contains the actual data, while the `class` object provides metadata about the object type. Different non-primitive classes have different storage types, such as `WideString` uses `int[]` and `ByteString` uses `byte[]`.

![Non-Primitive Object Representation, Example: `WideString`, `ByteArray`, `ByteString`](img/graal-fmc-nativeobject.drawio.png)

We want to investigate if we can improve the performance of string operations by leveraging tools provided by the Truffle framework.

### Baseline Performance
<!-- JSON Benchmark -->
<!-- Run on Antonys Computer -->
<!-- Results -->

To compare the performance of string operations, we decided to use the `JSON Benchmark` from the "Are We Fast Yet?" framework. We measure the time needed to parse 100 JSON strings and convert them into a Smalltalk object. We run the benchmark 300 times to ensure consistent results and to account for any warm-up effects.

The command to run the benchmark is as follows:

```bash
trufflesqueak --experimental-options --smalltalk.disable-startup --smalltalk.disable-interrupts --engine.Mode=default --code "AWFYHarness run: #('Json' 300 100)"
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
In the first experiment, we replaced the `byte[]` storage of `ByteString`  with `TruffleString`. With that change, we replaced byte operations with TruffleString operations.

### Results

<!-- Performance decreased -->


Let's compare the results of the first experiment with the baseline performance:

| Metric       | Baseline  | Experiment 1 |
| ------------ | --------- | ------------ |
| Average Time | 201.466ms | 327.14ms     |
| Minimum Time | 173 ms    | 291 ms       |
| Maximum Time | 1 532 ms  | 2 883    ms  |
| Summary Time | 60 440 ms | 98 142    ms |

We can see that the performance of the first experiment decreased compared to the baseline. The average time increased from 201.466ms to 327.14ms, and the maximum time increased significantly from 1 532ms to 2 883ms.

### Discussion
<!-- Codesize increased -->
<!-- Compilation time and code size of string comparisons increased -->

<!-- Issue: Provide for each permutation of string types a separate method to avoid the overhead of type checks -->
<!-- Reduce permutation by replacing ByteArrays with TruffleString -->

## Experiment 2: Replace ByteArray with TruffleString

### Implementation

<!-- Changed storage of ByteArray to TruffleString -->

In the second experiment, we extended the implementation of the first experiment. We also replaced the `byte[]` storage of `ByteArray` with `TruffleString` and used the same TruffleString operations as in the first experiment on `ByteArray`.

### Results

<!-- Performance improved to v1 -->
Let's compare the results of the second experiment with the baseline performance and the first experiment:

| Metric       | Baseline  | Experiment 1 | Experiment 2 |
| ------------ | --------- | ------------ | ------------ |
| Average Time | 201.466ms | 327.14ms     | 292.2ms      |
| Minimum Time | 173 ms    | 291 ms       | 261  ms      |
| Maximum Time | 1 532 ms  | 2 883    ms  | 2 393  ms    |
| Summary Time | 60 440 ms | 98 142    ms | 87 660  ms   |

We can see that the performance of the second experiment improved compared to the first experiment. The average time decreased from 327.14ms to 292.2ms, and the maximum time decreased from 2 883ms to 2 393ms.

In comparison to the baseline performance, the second experiment still shows a performance decrease, but it is an improvement over the first experiment.

### Discussion

<!-- Codesize decreased to v1 -->

<!-- Performance decreased compared to original -->
<!-- Compilation time and code size of string comparisons decreased -->

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