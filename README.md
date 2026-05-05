# GSoC 2026 — OpenPrinting
**Organization:** Linux Foundation / OpenPrinting  
## Fuzz and Test the go-mfp CPython Binding

The go-mfp cpython package is a Go library that embeds CPython, enabling multiple isolated Python sub-interpreters with automatic garbage collection. As it evolves into a standalone and potentially critical Linux component, reliability and security across Python 3.8 to the latest versions are key priorities.

This project focuses on building a robust testing ecosystem, including unit tests and fuzz tests for all components. It leverages Go's native fuzzing framework, ensures compatibility across Python versions and architectures (x86 and ARM64), and establishes CI pipelines along with clear documentation for maintaining and extending the test suite.

**Project Repository:** [OpenPrinting/go-mfp](https://github.com/OpenPrinting/go-mfp)
