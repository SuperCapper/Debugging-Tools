Memory problems are among the hardest failures to diagnose through ordinary logs because the allocation and the crash may be separated by hours.

Heap snapshots, allocation profiles, and runtime memory statistics show which objects remain in memory, how they are connected, and which references prevent garbage collection.

This helps distinguish a true leak from legitimate temporary growth. A process may use more memory because it is handling larger workloads, caching intentionally, or waiting for garbage collection. A leak exists when objects remain reachable after their useful lifetime has ended.

Common causes include event listeners that are never removed, timers that retain request context, unbounded maps, caches without eviction, closures holding large objects, and arrays that collect history indefinitely.

The largest object is not always the real cause. Retainer paths matter because they reveal why the object remains alive. A small global collection may indirectly retain a large graph of request and response data.

Memory debugging also requires observing behavior over time. A snapshot from one moment is less informative than comparisons taken before and after repeated workloads. If the same object categories continue growing after the operation should have released them, the investigation has a useful direction.

Process restarts can hide memory problems operationally, but they do not remove the underlying risk. As traffic grows, the restart interval becomes shorter, latency becomes unstable during garbage collection, and users experience failures during termination.

Heap analysis turns "the service uses too much memory" into a concrete question about which objects remain and who is still holding them.
