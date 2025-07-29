# TruffleString Experiment

> This document outlines the experiments conducted with the TruffleString class, including performance benchmarks, memory usage analysis, and other relevant findings.

## Introduction

### Background

<!-- How primitives and non primitives are represented -->
<!-- TruffleString class and its role in the Truffle framework -->

### Baseline Performance
<!-- JSON Benchmark -->
<!-- Run on Antonys Computer -->
<!-- Results -->

### Experiment Goals
<!-- Improved performance for string operations -->
<!-- Sideproduct: Improved interoperability with other languages -->

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