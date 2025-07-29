# Related Work

> This document provides a collection of papers and resources related to the project, including research papers, technical reports, and other relevant publications. They helped us understand the context and background of the project.

## Virtual Machines & Applications

- [The Architecture of Virtual Machines](https://minds.wisconsin.edu/bitstream/handle/1793/11154/file_1.pdf;jsessionid=9693E61A05F6E2A17502C38D9BC6202C?sequence=1): Gives a great overview over the Architecture of VMs.
- [Disentangling Virtual Machine Architecture](https://minds.wisconsin.edu/bitstream/handle/1793/11154/file_1.pdf;jsessionid=9693E61A05F6E2A17502C38D9BC6202C?sequence=1): Tries to find a common ground for virtual machine architecture

## Explanations for JIT and the Graal Compiler

- [YouTube: Just In Time (JIT) Compiler](https://youtu.be/d7KHAVaX_Rs): Great introduction about what JIT compilation is
- [Deep Dive Into the New Java JIT Compiler – Graal](https://www.baeldung.com/graal-java-jit-compiler): More detailed explanation on JVM Client Compiler (C1) and Server Compiler (C2) and optimization. Second part is about Graal Compiler.
- [Anatomy of Oracle GraalVM](https://www.oracle.com/a/ocom/docs/graalvm-enterprise-product-architecture.pdf): Compares GraalVM Ahead-of-Time (AOT) compilation with Just-In-Time (JIT) compilation.
- [Understanding How Graal Works - a Java JIT Compiler Written in Java](https://chrisseaton.com/truffleruby/jokerconf17/): Detailed explanation of the GraalVM architecture and how it works with Truffle.
- [One VM to Rule them all](https://www.researchgate.net/publication/262170315_One_VM_to_rule_them_all): Overview over GraalVM technical architecture and its components, i.e. Truffle.
- [Futamura Compiler and GraalVM](https://www.jfokus.se/jfokus23-preso/Dr-Futamura-and-the-Projection-Machine.pdf): Theoretical approach to build compiler generator and partial evaluation.
- [Java Hotspot HSDIS](https://blogs.oracle.com/javamagazine/post/java-hotspot-hsdis-disassembler): Introduces a Disassambler for Hotstop and Explanations for JIT, C1 and C2 compilation.

## TruffleSqueak

- [Exploratory tool-building platforms for polyglot virtual machines, Niephaus, 2022](https://publishup.uni-potsdam.de/frontdoor/index/index/docId/57177): Discusses the TruffleSqueak project and its implementation of Squeak/Smalltalk as a guest language using the Truffle framework.

## Other

- [Cross-language compiler benchmarking: are we fast yet?](https://dl.acm.org/doi/10.1145/2989225.2989232): Framework for cross-language compiler benchmarking, which we used to benchmark our implementation.
- [TruffleStrings: a Highly Optimized
Cross-Language String Implementation](https://graalworkshop.github.io/2022/slides/4_TruffleStrings.pdf): Presentation about the TruffleString class, which we used as a reference for our implementation.
