---
name: dynamic-analysis
description: Dynamic analysis during execution detects memory leaks (RAM not freed, worsening response time), wild pointers (stale references causing crashes/corruption), and performance profiling using Pareto 80/20 principle. Start early in development.
type: rule
chapter: "3"
bloom: K3
priority: HIGH
syllabus: TTA-3.5
---

# Dynamic Analysis

## Definition

Dynamic analysis examines software **during execution** to detect runtime defects that static analysis cannot find. It requires running the software with instrumented tools that observe actual behavior, memory usage, and performance.

---

## Memory Leaks

### Definition
A **memory leak** occurs when a program allocates memory (RAM) but fails to release it when it is no longer needed. The leaked memory remains allocated until the process terminates.

### Behavior Over Time
- Memory consumption increases continuously during program execution
- System response time worsens as available memory decreases
- Eventually: performance degradation → out-of-memory errors → process crash

### Detection
Dynamic analysis tools monitor:
- Every `malloc/new` allocation call
- Every `free/delete` deallocation call
- Allocations that exist at program termination without corresponding deallocation

### Tools
- **Valgrind Memcheck** (Linux/C/C++): Tracks every allocation/deallocation
- **AddressSanitizer (ASan)**: Compiler-instrumented memory error detection
- **Heap Profilers**: Java VisualVM, .NET CLR Profiler
- **LeakSanitizer (LSan)**: Standalone leak detection

### Symptoms in Production
- Worsening response time on long-running processes
- Server requiring periodic restart to recover performance
- Out-of-memory crashes after extended operation

---

## Wild Pointers

### Definition
A **wild pointer** (also: stale pointer, dangling pointer) is a pointer that references memory that has already been freed or that was never validly allocated.

### Causes
- **Use-after-free**: Memory is freed but the pointer is still used
- **Uninitialized pointer**: Pointer variable used without being assigned
- **Pointer to stack variable**: Returning a pointer to a local variable (which is freed when function returns)
- **Double free**: Memory freed twice — second free corrupts the allocator

### Consequences
- Reading from wild pointer: returns garbage data → data corruption
- Writing to wild pointer: corrupts arbitrary memory → crashes, security vulnerabilities
- Behavior is non-deterministic (depends on what was allocated to that memory after freeing)

### Detection Tools
- **AddressSanitizer (ASan)**: Detects use-after-free, buffer overflows
- **Valgrind Memcheck**: Detects invalid reads/writes
- **Purify**: Commercial tool for memory error detection
- **Static analysis**: Can detect some patterns (uk anomaly in data flow analysis)

---

## Performance Profiling

### Pareto Principle (80/20 Rule)
Approximately **80% of execution time** is typically spent in **20% of the code**. Dynamic analysis (profiling) identifies this critical 20%.

### Profiling Types

| Type | What It Measures | Use Case |
|---|---|---|
| CPU profiling | Time spent in each function | Identify CPU bottlenecks |
| Memory profiling | Memory allocated by each function | Identify allocation hotspots |
| I/O profiling | Disk/network I/O per operation | Identify I/O bottlenecks |
| Call profiling | Call frequency and call graph | Identify frequently called functions |

### Profiling Approaches
- **Sampling**: Periodic snapshot of call stack (low overhead)
- **Instrumentation**: Insert measurement code at each function entry/exit (high accuracy, higher overhead)

### Process
1. Run the application under a realistic workload
2. Collect profiling data
3. Identify the top 20% of functions by resource consumption
4. Optimize those functions first (highest impact per effort)
5. Re-profile to verify improvement

---

## When to Start Dynamic Analysis

**Start early** — dynamic analysis should begin at the component/unit testing level, not wait for system testing:

| Phase | Dynamic Analysis Activity |
|---|---|
| Component testing | Memory and pointer analysis on individual modules |
| Integration testing | Detect leaks and pointer issues at integration points |
| System testing | Full performance profiling under realistic load |
| Regression testing | Re-run analysis after changes to detect regressions |

**Why start early?**
- Memory leaks found at component level are cheap to fix
- Memory leaks found in production require emergency patches
- Root cause analysis is much simpler when the component is isolated

---

## Key Points

- Dynamic analysis requires **code execution** with instrumented tools
- **Memory leaks**: Allocated RAM not freed → worsening response time → crash
- **Wild pointers**: Stale/freed pointer accessed → data corruption or crash
- **Performance profiling**: Pareto 80/20 → optimize the 20% of code consuming 80% of resources
- Start dynamic analysis at component level, not system level
- Tools: Valgrind, AddressSanitizer, profilers (gprof, perf, VisualVM, py-spy)
