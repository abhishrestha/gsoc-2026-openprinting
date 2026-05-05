# GSoC 2026 — Fuzz and Test the go-mfp CPython Binding

**Student:** Abhishrestha Tiwari  
**Organization:** Linux Foundation / OpenPrinting  
**Mentor:** Alexander Pevzner, Till Kamppeter  
**Project:** Fuzz and Test the go-mfp CPython Binding  

## About the Project

The go-mfp cpython package is a unique Go library that embeds CPython 
as a scripting engine. This project builds a comprehensive unit test 
and fuzz test suite for the package across Python 3.8–latest on both 
x86 and ARM64.

## Contributions

- [PR #21 — Fix ARM64 deadlock in cpython.Python.Close()](https://github.com/OpenPrinting/go-mfp/pull/21) ✅ Merged
- [PR #50 — Add unit tests for error types](https://github.com/OpenPrinting/go-mfp/pull/50) Under Review

## Weekly Updates

### Week 1 — Community Bonding (May 1–7, 2026)

**What I did:**
- Set up Lima VM (Ubuntu 25.10, aarch64) with all dependencies — Go, CPython, cgo toolchain
- Ran coverage audit on the cpython package — overall coverage: 77.7%
- Identified all functions at 0% coverage across error.go, gate.go, object.go, and python.go
- Created `error_test.go` — a unit test suite for `error.go` in the cpython package
- Tests cover all 6 error types: ErrPython, ErrTypeConversion, ErrOverflow, ErrClosed, ErrInvalidObject, ErrNotFound
- Achieved 100% test coverage for error.go (previously 0%)
- Submitted PR #50 and addressed Alexander's review feedback (copyright attribution, removing unintended python.go formatting changes)
- Synced local repo with upstream master to pick up latest code changes (new `except` field in ErrPython)
- Updated tests to match the new ErrPython format and verified all 8 tests pass
- Set up Go static analysis tools: go vet, staticcheck
- Configured GitHub authentication (Personal Access Token) for pushing to fork

**Coverage improvement:**
- error.go: 0% → 100%
- Overall:  77.7% → 78.3% 

**What I learned:**
- Go testing framework — writing unit tests with `testing.T` and table-driven test patterns
- How the cpython package error types implement Go's `error` interface
- Git workflow for contributing to open-source: fork → branch → PR → review → fix → push
- Importance of following project code style — Alexander uses golint, go vet, and staticcheck with zero warnings expected
- Each PR should be logically isolated and only touch relevant files

**Challenges faced:**
- VS Code Remote-SSH connection to Lima VM timed out due to network issues inside VM — used terminal-based micro editor as alternative
- Upstream code changed between starting work and submitting PR — had to rebase and update tests for new ErrPython struct (added `except` field)
- Accidentally included python.go formatting changes in the PR — learned to verify `git diff` before committing

**Next steps:**
- Get PR #50 merged
- Write fuzz tests for error.go (`error_fuzz_test.go`)
- Start unit tests for gate.go — has the most functions at 0% coverage (lastErrorLocation, typemodulename, setattr, getListItem, getTupleItem)
- Continue with object.go and python.go unit tests
