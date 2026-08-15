When a process consumes high CPU or becomes unresponsive, reading the code is rarely enough to identify the real cost.

CPU profilers sample what the process is executing over time and show which functions consume the largest share. Flame graphs turn that data into a visual representation of call stacks and accumulated work.

This is useful because expensive behavior may come from ordinary operations repeated at scale. JSON serialization, schema validation, regular expressions, object copying, date formatting, compression, or logging can dominate CPU without any one call appearing suspicious.

A profiler can also disprove assumptions. The team may spend hours optimizing a database query while the process is actually occupied transforming the result. A suspected algorithm may be insignificant compared with a library function called inside a tight loop.

Profiling should use realistic workloads. A function that dominates a synthetic benchmark may barely matter in production, while a small per-request cost can become enormous across high traffic.

I also compare profiles before and after optimization. A change that makes one function faster may simply move cost elsewhere or increase memory pressure. Performance work needs evidence that the complete request or workload improved.

A profiler replaces arguments about what seems expensive with measurements of what actually consumed execution time.
