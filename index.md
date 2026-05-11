# GSoC 2026 — Fuzzing & Testing the `go-mfp` CPython Binding

**Contributor:**  
Abhishrestha Tiwari

**Organization:**  
The Linux Foundation / OpenPrinting

**Mentors:**  
Alexander Pevzner, Till Kamppeter, ttfish

**Project:**  
*Fuzz and Test the `go-mfp` CPython Binding*

---

## About the Project

The `go-mfp/cpython` package is a Go library that embeds CPython as a scripting engine.
This project focuses on building a comprehensive testing and fuzzing infrastructure for the package across Python 3.8 through the latest versions on both x86 and ARM64 architectures.

The primary goals are:

* Improve unit test coverage
* Add fuzz testing for critical components
* Detect architecture-specific issues
* Ensure long-term reliability and maintainability

---

## Contributions

### Merged Pull Requests

* [PR #21 — Fix ARM64 deadlock in `cpython.Python.Close()`](https://github.com/OpenPrinting/go-mfp/pull/21) ✅
* [PR #50 — Add unit tests for error types](https://github.com/OpenPrinting/go-mfp/pull/50) ✅

---

# Work Completed

## Environment Setup

Configured a complete ARM64 development and testing environment using Lima VM.

### Stack Used

* Ubuntu 25.10 (aarch64)
* Go toolchain
* CPython
* cgo toolchain
* Lima VM

---

## Coverage Audit

Performed a detailed coverage analysis of the `cpython` package.

### Initial Findings

* Overall package coverage: **77.7%**
* Multiple functions had **0% coverage**
* Major uncovered areas:

* `except.go → except_test.go`
* `float.go → float_test.go `
* `gate.go → gate_test.go `
* `objid.go → objid_test.go `
* `reflect.go → reflect_test.go `

---

# Unit Testing Work

## Added

```text
cpython/error_test.go
```

Implemented a dedicated unit test suite for all error types in `error.go`.

### Covered Error Types

* `ErrPython`
* `ErrTypeConversion`
* `ErrOverflow`
* `ErrClosed`
* `ErrInvalidObject`
* `ErrNotFound`

---

## Results

| File       | Before | After |
| ---------- | ------ | ----- |
| `error.go` | 0%     | 100%  |

### Overall Package Coverage

```text
77.7% → 78.3%
```

All tests and static analysis checks passed successfully with zero warnings.

---

# Maintainer Review Improvements

Based on maintainer feedback, the following refinements were made:

* Replaced runtime interface checks with compile-time assertions

```go
var (
    _ error = ErrPython{}
)
```

* Updated tests after upstream changes introduced the `except` field in `ErrPython`
* Removed unrelated formatting changes accidentally included in the PR
* Aligned formatting and testing style with project conventions

---

# Validation & Quality Checks

Validated the implementation using:

```bash
go test -v ./cpython/...
golint ./cpython/...
go vet ./cpython/...
staticcheck ./cpython/...
```

### Standards Followed

* `golint`
* `go vet`
* `staticcheck`

All checks completed successfully without warnings.

---
```markdown
## Added
```text
cpython/except_test.go

```
Implemented a dedicated unit test suite for the `Except` type and exception constants in `except.go`.

### Covered
* `TestExceptConstants` — verifies all standard exception constants have correct string values
* `TestExceptObjectKnown` — verifies `object()` returns non-nil for all known standard exceptions
* `TestExceptObjectUnknown` — verifies `object()` falls back to `SystemError` for unknown exception names

---

## Results
| File        | Before | After |
| ----------- | ------ | ----- |
| `except.go` | 0%     | 100%  |

### Overall Package Coverage
```text
78.3% → 78.9%
```
All tests and static analysis checks passed successfully with zero warnings.
```

# Development Workflow

## Branch Strategy

Using one branch per logical change:

```text
error-tests
gate-tests
object-tests
python-tests
error-fuzz-tests
```

---

## PR Strategy

Keeping pull requests:

* Small
* Focused
* Logically isolated

Separate PRs are submitted for:

* Unit tests
* Fuzz tests
* Coverage improvements

---

# Current Focus

Ongoing work includes:

* Expanding unit test coverage for remaining files
* Adding fuzz testing for critical APIs
* Improving ARM64 stability and reproducibility
* Increasing overall package coverage further
