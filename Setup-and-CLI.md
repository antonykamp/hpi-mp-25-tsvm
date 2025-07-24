# Setup and Common Commands

> This document provides a collection of common command line options we used with GraalVM and Truffle on TruffleSqueak.

## Setup GraalVM

Follow the GraalVM installation guide [3] for step-by-step instructions on installing GraalVM. The installation guide provides instructions for different operating systems.

## Setup TruffleSqueak

Follow the TruffleSqueak setup guide [2] for step-by-step instructions on setting up the TruffleSqueak project. The setup guide provides instructions for different operating systems and IDEs.

To build the TruffleSqueak executable, we use the `⁠mx` tool, which is part of the GraalVM ecosystem [1]. We call `mx` when the current working directory is the `trufflesqueak` directory with `../mx/mx`.

## Export GraalVM Home

Before running any commands, you need to set the `GRAALVM_HOME` environment variable to point to your GraalVM installation. You can do this by running the following command in your terminal:

```bash
export GRAALVM_HOME=$(mx --dy /compiler graalvm-home) 
```

## Build

We use the `mx` tool to build the TruffleSqueak project. Before building the project, you need to ensure that `GRAALVM_HOME` is set correctly. The command below builds the TruffleSqueak.

```bash
mx --dy trufflesqueak,/compiler build
```

## Run

To run an image, we use the built artifacts. You can run an image with the following command:

```bash
$GRAALVM_HOME/bin/trufflesqueak images/test-64bit.image 
```

## Debugging

To debug the image, add these flags to your *build* or *run* command:

```bash
--vm.agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=8000
```

Connect your debugger to port 8000 to start troubleshooting your build process or image. We recommend using IntelliJ IDEA for debugging. You can find more information about setting up your IDE in the `mx` documentation [4].

### Benchmark

We ran the JSON benchmark from the Are We Yet framework (AWFY) Framework to measure the performance of the TruffleSqueak implementation [5]. The command below runs the benchmark with specific options:

```bash
$GRAALVM_HOME/bin/trufflesqueak --experimental-options --smalltalk.disable-startup --smalltalk.disable-interrupts --engine.Mode=default --engine.TraceCompilation --compiler.TracePerformanceWarnings=call,instanceof,store,trivial --engine.CompilationFailureAction=Print --engine.CompilationStatistics --log.file="./Json.trace.log" --quiet --code "AWFYHarness run: #('Json' 300 100)" 
```

You can find the compilation trace log in the `Json.trace.log` file.

### Ideal Graph Visualizer (IGV)

The IGV is an application that allows developers to visualize the Intermediate Representation (IR) of the code during different phases of the compilation process. To open IGV, you can use the following command:

```bash
cd graal/compiler
../../mx/mx igv
```

You have to dump the IR before you can visualize it. You can do this by adding the following flags to the run command:

```bash
--vm.Dgraal.Dump=Truffle:1 --engine.MultiTier=false --engine.TraceCompilation
```

You can find the dumped IR in the `trufflesqueak/graal_dumps` directory. Each file contains the IR for a specific method.

### Test

To run a Squeak unittest test, you can use the following command. In this example, we run the `BitmapStreamTests>>testShortIntegerArrayWithSmartRefStreamOnDisk` test:

```bash
../mx/mx  --env trufflesqueak-jvm unittest --use-graalvm -DsqueakTests="BitmapStreamTests>>testShortIntegerArrayWithSmartRefStreamOnDisk" SqueakSUnitTest
```

## Resources

- [1] [MX Documentation](https://github.com/graalvm/mx/tree/master/docs)
- [2] [TruffleSqueak Documentation](https://github.com/hpi-swa/trufflesqueak/blob/main/docs/development.md)
- [3] [Getting Started with Oracle GraalVM](https://github.com/oracle/graal/blob/master/docs/getting-started/get-started.md)
- [4] [MX IDE Setup](https://github.com/graalvm/mx/blob/master/docs/IDE.md)
- [5] [Cross-language compiler benchmarking: are we fast yet?](https://dl.acm.org/doi/10.1145/2989225.2989232)

State: 2025-07-24
