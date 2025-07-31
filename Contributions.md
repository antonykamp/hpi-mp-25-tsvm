# Contributions

> This document outlines the contributions made to the project, including code changes, documentation updates, and other enhancements.

## TruffleString Experiment

- Pull request including the experiment replacing `ByteString` and `ByteArray` with `TruffleString`: [hpi-swa/trufflesqueak#199](https://github.com/hpi-swa/trufflesqueak/pull/199).
- Issue including the experiment protocol: [hpi-swa/trufflesqueak#203](https://github.com/hpi-swa/trufflesqueak/issues/203)

## LCTLCT (Legendary compilation trace log comparison tool)

- LCTLCT is introduced in the following repository: [Olliwehr/LCTLCT](https://github.com/Olliwehr/LCTLCT)
- The documentation shows typical use-cases of the tool.
- For further information/help, you can also use the `-h` CLI option as the Python script makes uses of CLI arguments via the `argparse` library.

## Future Work (Issues)

- TruffleSqueak
  - Experiment: Introduce TruffleString with higher level string functions [hpi-swa/trufflesqueak#204](https://github.com/hpi-swa/trufflesqueak/issues/204)
  - Inspect Truffle Objects in IntelliJ [hpi-swa/trufflesqueak#205](https://github.com/hpi-swa/trufflesqueak/issues/205)
- Graal
  - Structured textual output for compilation traces and compilation statistics [oracle/graal#11837](https://github.com/oracle/graal/issues/11837)
  - Add Syntax and Static Type Analysis to Truffle Specialization Guards [oracle/graal#11838](https://github.com/oracle/graal/issues/11838)
- LCTLCT
  - [Future work: Integration ideas #1](https://github.com/Olliwehr/LCTLCT/issues/1)
    - Currently, the tool is a standalone Python script, which is dependent on CLI arguments.
    - In order to avoid frequent window and context switches between the terminal and other tools/the IDE, we think that it is beneficial if the tool could offer more integration points
      (e.g. to the [`mx` CLI tool](https://github.com/graalvm/mx)).
  - [Future work: Explore full-other-join character for diffing mechanism #2](https://github.com/Olliwehr/LCTLCT/issues/2)
    - For the diffing mechanism, that aggregates metric-specific differences between two compilation traces,
      currently, only compilation occurrences of a method are considered that can be found in both traces.
      The reason for that is simply that by that we always have reliable metric values to compare.
    - However, we think it is worth to explore the possibility to employ (in analogy to SQL) a "full-other-join" character for the diffing.
      That could achieve more insights regarding the specified metric as all compilation occurrences are to be diffed.
      On the other hand, meaningful "blank" values need to be chosen as the question remains whether it is really suitable to just fill in the blanks with zeros,
      which is also something that could differ between the available metrics.

## Documentation

- Pull request including the development documentation updates: [hpi-swa/trufflesqueak#202](https://github.com/hpi-swa/trufflesqueak/pull/202).
