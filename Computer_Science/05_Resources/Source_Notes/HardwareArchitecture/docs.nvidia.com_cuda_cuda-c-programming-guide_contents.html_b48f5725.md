Title: Contents â CUDA C++ Programming Guide
Mapped Topic: GPU execution model
Source URL: https://docs.nvidia.com/cuda/cuda-c-programming-guide/contents.html
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:04:47+00:00
Mapped From CSE.md Section: Part 2: A. Hardware, CPU, GPU, architecture, chip basics

# Content

# Contents[ï](https://docs.nvidia.com#contents)

[1. Overview](https://docs.nvidia.com/index.html)[2. What Is the CUDA C Programming Guide?](https://docs.nvidia.com/index.html#what-is-the-cuda-c-programming-guide)-
[3. Introduction](https://docs.nvidia.com/index.html#introduction) [4. Changelog](https://docs.nvidia.com/index.html#changelog)-
[5. Programming Model](https://docs.nvidia.com/index.html#programming-model) -
[6. Programming Interface](https://docs.nvidia.com/index.html#programming-interface)-
[6.1. Compilation with NVCC](https://docs.nvidia.com/index.html#compilation-with-nvcc) -
[6.2. CUDA Runtime](https://docs.nvidia.com/index.html#cuda-runtime)[6.2.1. Initialization](https://docs.nvidia.com/index.html#initialization)[6.2.2. Device Memory](https://docs.nvidia.com/index.html#device-memory)-
[6.2.3. Device Memory L2 Access Management](https://docs.nvidia.com/index.html#device-memory-l2-access-management)[6.2.3.1. L2 Cache Set-Aside for Persisting Accesses](https://docs.nvidia.com/index.html#l2-cache-set-aside-for-persisting-accesses)[6.2.3.2. L2 Policy for Persisting Accesses](https://docs.nvidia.com/index.html#l2-policy-for-persisting-accesses)[6.2.3.3. L2 Access Properties](https://docs.nvidia.com/index.html#l2-access-properties)[6.2.3.4. L2 Persistence Example](https://docs.nvidia.com/index.html#l2-persistence-example)[6.2.3.5. Reset L2 Access to Normal](https://docs.nvidia.com/index.html#reset-l2-access-to-normal)[6.2.3.6. Manage Utilization of L2 set-aside cache](https://docs.nvidia.com/index.html#manage-utilization-of-l2-set-aside-cache)[6.2.3.7. Query L2 cache Properties](https://docs.nvidia.com/index.html#query-l2-cache-properties)[6.2.3.8. Control L2 Cache Set-Aside Size for Persisting Memory Access](https://docs.nvidia.com/index.html#control-l2-cache-set-aside-size-for-persisting-memory-access)

[6.2.4. Shared Memory](https://docs.nvidia.com/index.html#shared-memory)[6.2.5. Distributed Shared Memory](https://docs.nvidia.com/index.html#distributed-shared-memory)-
[6.2.6. Page-Locked Host Memory](https://docs.nvidia.com/index.html#page-locked-host-memory) -
[6.2.7. Memory Synchronization Domains](https://docs.nvidia.com/index.html#memory-synchronization-domains) -
[6.2.8. Asynchronous Concurrent Execution](https://docs.nvidia.com/index.html#asynchronous-concurrent-execution)[6.2.8.1. Concurrent Execution between Host and Device](https://docs.nvidia.com/index.html#concurrent-execution-between-host-and-device)[6.2.8.2. Concurrent Kernel Execution](https://docs.nvidia.com/index.html#concurrent-kernel-execution)[6.2.8.3. Overlap of Data Transfer and Kernel Execution](https://docs.nvidia.com/index.html#overlap-of-data-transfer-and-kernel-execution)[6.2.8.4. Concurrent Data Transfers](https://docs.nvidia.com/index.html#concurrent-data-transfers)-
[6.2.8.5. Streams](https://docs.nvidia.com/index.html#streams) -
[6.2.8.6. Programmatic Dependent Launch and Synchronization](https://docs.nvidia.com/index.html#programmatic-dependent-launch-and-synchronization) -
[6.2.8.7. CUDA Graphs](https://docs.nvidia.com/index.html#cuda-graphs)-
[6.2.8.7.1. Graph Structure](https://docs.nvidia.com/index.html#graph-structure) [6.2.8.7.2. Creating a Graph Using Graph APIs](https://docs.nvidia.com/index.html#creating-a-graph-using-graph-apis)-
[6.2.8.7.3. Creating a Graph Using Stream Capture](https://docs.nvidia.com/index.html#creating-a-graph-using-stream-capture) [6.2.8.7.4. CUDA User Objects](https://docs.nvidia.com/index.html#cuda-user-objects)-
[6.2.8.7.5. Updating Instantiated Graphs](https://docs.nvidia.com/index.html#updating-instantiated-graphs) [6.2.8.7.6. Using Graph APIs](https://docs.nvidia.com/index.html#using-graph-apis)-
[6.2.8.7.7. Device Graph Launch](https://docs.nvidia.com/index.html#device-graph-launch) -
[6.2.8.7.8. Conditional Graph Nodes](https://docs.nvidia.com/index.html#conditional-graph-nodes)

-
-
[6.2.8.8. Events](https://docs.nvidia.com/index.html#events) [6.2.8.9. Synchronous Calls](https://docs.nvidia.com/index.html#synchronous-calls)

-
[6.2.9. Multi-Device System](https://docs.nvidia.com/index.html#multi-device-system) [6.2.10. Unified Virtual Address Space](https://docs.nvidia.com/index.html#unified-virtual-address-space)[6.2.11. Interprocess Communication](https://docs.nvidia.com/index.html#interprocess-communication)[6.2.12. Error Checking](https://docs.nvidia.com/index.html#error-checking)[6.2.13. Call Stack](https://docs.nvidia.com/index.html#call-stack)-
[6.2.14. Texture and Surface Memory](https://docs.nvidia.com/index.html#texture-and-surface-memory) -
[6.2.15. Graphics Interoperability](https://docs.nvidia.com/index.html#graphics-interoperability) -
[6.2.16. External Resource Interoperability](https://docs.nvidia.com/index.html#external-resource-interoperability)-
[6.2.16.1. Vulkan Interoperability](https://docs.nvidia.com/index.html#vulkan-interoperability)[6.2.16.1.1. Matching device UUIDs](https://docs.nvidia.com/index.html#matching-device-uuids)[6.2.16.1.2. Importing Memory Objects](https://docs.nvidia.com/index.html#importing-memory-objects)[6.2.16.1.3. Mapping Buffers onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-buffers-onto-imported-memory-objects)[6.2.16.1.4. Mapping Mipmapped Arrays onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-mipmapped-arrays-onto-imported-memory-objects)[6.2.16.1.5. Importing Synchronization Objects](https://docs.nvidia.com/index.html#importing-synchronization-objects)[6.2.16.1.6. Signaling/Waiting on Imported Synchronization Objects](https://docs.nvidia.com/index.html#signaling-waiting-on-imported-synchronization-objects)

[6.2.16.2. OpenGL Interoperability](https://docs.nvidia.com/index.html#opengl-interoperability-ext-res-int)-
[6.2.16.3. Direct3D 12 Interoperability](https://docs.nvidia.com/index.html#direct3d-12-interoperability)[6.2.16.3.1. Matching Device LUIDs](https://docs.nvidia.com/index.html#matching-device-luids)[6.2.16.3.2. Importing Memory Objects](https://docs.nvidia.com/index.html#importing-memory-objects-dir3d-12-int)[6.2.16.3.3. Mapping Buffers onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-buffers-onto-imported-memory-objects-dir3d-12-int)[6.2.16.3.4. Mapping Mipmapped Arrays onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-mipmapped-arrays-onto-imported-memory-objects-dir3d-12-int)[6.2.16.3.5. Importing Synchronization Objects](https://docs.nvidia.com/index.html#importing-synchronization-objects-dir3d-12-int)[6.2.16.3.6. Signaling/Waiting on Imported Synchronization Objects](https://docs.nvidia.com/index.html#signaling-waiting-on-imported-synchronization-objects-dir3d-12-int)

-
[6.2.16.4. Direct3D 11 Interoperability](https://docs.nvidia.com/index.html#direct3d-11-interoperability)[6.2.16.4.1. Matching Device LUIDs](https://docs.nvidia.com/index.html#matching-device-luids-dir3d-11-int)[6.2.16.4.2. Importing Memory Objects](https://docs.nvidia.com/index.html#importing-memory-objects-dir3d-11-int)[6.2.16.4.3. Mapping Buffers onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-buffers-onto-imported-memory-objects-dir3d-11-int)[6.2.16.4.4. Mapping Mipmapped Arrays onto Imported Memory Objects](https://docs.nvidia.com/index.html#mapping-mipmapped-arrays-onto-imported-memory-objects-dir3d-11-int)[6.2.16.4.5. Importing Synchronization Objects](https://docs.nvidia.com/index.html#importing-synchronization-objects-dir3d-11-int)[6.2.16.4.6. Signaling/Waiting on Imported Synchronization Objects](https://docs.nvidia.com/index.html#signaling-waiting-on-imported-synchronization-objects-dir3d-11-int)

-
[6.2.16.5. NVIDIA Software Communication Interface Interoperability (NVSCI)](https://docs.nvidia.com/index.html#nvidia-software-communication-interface-interoperability-nvsci)

-

[6.3. Versioning and Compatibility](https://docs.nvidia.com/index.html#versioning-and-compatibility)[6.4. Compute Modes](https://docs.nvidia.com/index.html#compute-modes)[6.5. Mode Switches](https://docs.nvidia.com/index.html#mode-switches)[6.6. Tesla Compute Cluster Mode for Windows](https://docs.nvidia.com/index.html#tesla-compute-cluster-mode-for-windows)

-
-
[7. Hardware Implementation](https://docs.nvidia.com/index.html#hardware-implementation) -
[8. Performance Guidelines](https://docs.nvidia.com/index.html#performance-guidelines) [9. CUDA-Enabled GPUs](https://docs.nvidia.com/index.html#cuda-enabled-gpus)-
[10. C++ Language Extensions](https://docs.nvidia.com/index.html#c-language-extensions)-
[10.1. Function Execution Space Specifiers](https://docs.nvidia.com/index.html#function-execution-space-specifiers) -
[10.2. Variable Memory Space Specifiers](https://docs.nvidia.com/index.html#variable-memory-space-specifiers) -
[10.3. Built-in Vector Types](https://docs.nvidia.com/index.html#built-in-vector-types) -
[10.4. Built-in Variables](https://docs.nvidia.com/index.html#built-in-variables) [10.5. Memory Fence Functions](https://docs.nvidia.com/index.html#memory-fence-functions)[10.6. Synchronization Functions](https://docs.nvidia.com/index.html#synchronization-functions)[10.7. Mathematical Functions](https://docs.nvidia.com/index.html#mathematical-functions)-
[10.8. Texture Functions](https://docs.nvidia.com/index.html#texture-functions)-
[10.8.1. Texture Object API](https://docs.nvidia.com/index.html#texture-object-api-appendix)[10.8.1.1. tex1Dfetch()](https://docs.nvidia.com/index.html#tex1dfetch)[10.8.1.2. tex1D()](https://docs.nvidia.com/index.html#tex1d)[10.8.1.3. tex1DLod()](https://docs.nvidia.com/index.html#tex1dlod)[10.8.1.4. tex1DGrad()](https://docs.nvidia.com/index.html#tex1dgrad)[10.8.1.5. tex2D()](https://docs.nvidia.com/index.html#tex2d)[10.8.1.6. tex2D() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2d-for-sparse-cuda-arrays)[10.8.1.7. tex2Dgather()](https://docs.nvidia.com/index.html#tex2dgather)[10.8.1.8. tex2Dgather() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2dgather-for-sparse-cuda-arrays)[10.8.1.9. tex2DGrad()](https://docs.nvidia.com/index.html#tex2dgrad)[10.8.1.10. tex2DGrad() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2dgrad-for-sparse-cuda-arrays)[10.8.1.11. tex2DLod()](https://docs.nvidia.com/index.html#tex2dlod)[10.8.1.12. tex2DLod() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2dlod-for-sparse-cuda-arrays)[10.8.1.13. tex3D()](https://docs.nvidia.com/index.html#tex3d)[10.8.1.14. tex3D() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex3d-for-sparse-cuda-arrays)[10.8.1.15. tex3DLod()](https://docs.nvidia.com/index.html#tex3dlod)[10.8.1.16. tex3DLod() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex3dlod-for-sparse-cuda-arrays)[10.8.1.17. tex3DGrad()](https://docs.nvidia.com/index.html#tex3dgrad)[10.8.1.18. tex3DGrad() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex3dgrad-for-sparse-cuda-arrays)[10.8.1.19. tex1DLayered()](https://docs.nvidia.com/index.html#tex1dlayered)[10.8.1.20. tex1DLayeredLod()](https://docs.nvidia.com/index.html#tex1dlayeredlod)[10.8.1.21. tex1DLayeredGrad()](https://docs.nvidia.com/index.html#tex1dlayeredgrad)[10.8.1.22. tex2DLayered()](https://docs.nvidia.com/index.html#tex2dlayered)[10.8.1.23. tex2DLayered() for Sparse CUDA Arrays](https://docs.nvidia.com/index.html#tex2dlayered-for-sparse-cuda-arrays)[10.8.1.24. tex2DLayeredLod()](https://docs.nvidia.com/index.html#tex2dlayeredlod)[10.8.1.25. tex2DLayeredLod() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2dlayeredlod-for-sparse-cuda-arrays)[10.8.1.26. tex2DLayeredGrad()](https://docs.nvidia.com/index.html#tex2dlayeredgrad)[10.8.1.27. tex2DLayeredGrad() for sparse CUDA arrays](https://docs.nvidia.com/index.html#tex2dlayeredgrad-for-sparse-cuda-arrays)[10.8.1.28. texCubemap()](https://docs.nvidia.com/index.html#texcubemap)[10.8.1.29. texCubemapGrad()](https://docs.nvidia.com/index.html#texcubemapgrad)[10.8.1.30. texCubemapLod()](https://docs.nvidia.com/index.html#texcubemaplod)[10.8.1.31. texCubemapLayered()](https://docs.nvidia.com/index.html#texcubemaplayered)[10.8.1.32. texCubemapLayeredGrad()](https://docs.nvidia.com/index.html#texcubemaplayeredgrad)[10.8.1.33. texCubemapLayeredLod()](https://docs.nvidia.com/index.html#texcubemaplayeredlod)

-
-
[10.9. Surface Functions](https://docs.nvidia.com/index.html#surface-functions)-
[10.9.1. Surface Object API](https://docs.nvidia.com/index.html#surface-object-api-appendix)[10.9.1.1. surf1Dread()](https://docs.nvidia.com/index.html#surf1dread)[10.9.1.2. surf1Dwrite](https://docs.nvidia.com/index.html#surf1dwrite)[10.9.1.3. surf2Dread()](https://docs.nvidia.com/index.html#surf2dread)[10.9.1.4. surf2Dwrite()](https://docs.nvidia.com/index.html#surf2dwrite)[10.9.1.5. surf3Dread()](https://docs.nvidia.com/index.html#surf3dread)[10.9.1.6. surf3Dwrite()](https://docs.nvidia.com/index.html#surf3dwrite)[10.9.1.7. surf1DLayeredread()](https://docs.nvidia.com/index.html#surf1dlayeredread)[10.9.1.8. surf1DLayeredwrite()](https://docs.nvidia.com/index.html#surf1dlayeredwrite)[10.9.1.9. surf2DLayeredread()](https://docs.nvidia.com/index.html#surf2dlayeredread)[10.9.1.10. surf2DLayeredwrite()](https://docs.nvidia.com/index.html#surf2dlayeredwrite)[10.9.1.11. surfCubemapread()](https://docs.nvidia.com/index.html#surfcubemapread)[10.9.1.12. surfCubemapwrite()](https://docs.nvidia.com/index.html#surfcubemapwrite)[10.9.1.13. surfCubemapLayeredread()](https://docs.nvidia.com/index.html#surfcubemaplayeredread)[10.9.1.14. surfCubemapLayeredwrite()](https://docs.nvidia.com/index.html#surfcubemaplayeredwrite)

-
[10.10. Read-Only Data Cache Load Function](https://docs.nvidia.com/index.html#read-only-data-cache-load-function)[10.11. Load Functions Using Cache Hints](https://docs.nvidia.com/index.html#load-functions-using-cache-hints)[10.12. Store Functions Using Cache Hints](https://docs.nvidia.com/index.html#store-functions-using-cache-hints)[10.13. Time Function](https://docs.nvidia.com/index.html#time-function)-
[10.14. Atomic Functions](https://docs.nvidia.com/index.html#atomic-functions)-
[10.14.1. Arithmetic Functions](https://docs.nvidia.com/index.html#arithmetic-functions)[10.14.1.1. atomicAdd()](https://docs.nvidia.com/index.html#atomicadd)[10.14.1.2. atomicSub()](https://docs.nvidia.com/index.html#atomicsub)[10.14.1.3. atomicExch()](https://docs.nvidia.com/index.html#atomicexch)[10.14.1.4. atomicMin()](https://docs.nvidia.com/index.html#atomicmin)[10.14.1.5. atomicMax()](https://docs.nvidia.com/index.html#atomicmax)[10.14.1.6. atomicInc()](https://docs.nvidia.com/index.html#atomicinc)[10.14.1.7. atomicDec()](https://docs.nvidia.com/index.html#atomicdec)[10.14.1.8. atomicCAS()](https://docs.nvidia.com/index.html#atomiccas)[10.14.1.9. __nv_atomic_exchange()](https://docs.nvidia.com/index.html#nv-atomic-exchange)[10.14.1.10. __nv_atomic_exchange_n()](https://docs.nvidia.com/index.html#nv-atomic-exchange-n)[10.14.1.11. __nv_atomic_compare_exchange()](https://docs.nvidia.com/index.html#nv-atomic-compare-exchange)[10.14.1.12. __nv_atomic_compare_exchange_n()](https://docs.nvidia.com/index.html#nv-atomic-compare-exchange-n)[10.14.1.13. __nv_atomic_fetch_add() and __nv_atomic_add()](https://docs.nvidia.com/index.html#nv-atomic-fetch-add-and-nv-atomic-add)[10.14.1.14. __nv_atomic_fetch_sub() and __nv_atomic_sub()](https://docs.nvidia.com/index.html#nv-atomic-fetch-sub-and-nv-atomic-sub)[10.14.1.15. __nv_atomic_fetch_min() and __nv_atomic_min()](https://docs.nvidia.com/index.html#nv-atomic-fetch-min-and-nv-atomic-min)[10.14.1.16. __nv_atomic_fetch_max() and __nv_atomic_max()](https://docs.nvidia.com/index.html#nv-atomic-fetch-max-and-nv-atomic-max)

-
[10.14.2. Bitwise Functions](https://docs.nvidia.com/index.html#bitwise-functions) -
[10.14.3. Other atomic functions](https://docs.nvidia.com/index.html#other-atomic-functions)

-
-
[10.15. Address Space Predicate Functions](https://docs.nvidia.com/index.html#address-space-predicate-functions) -
[10.16. Address Space Conversion Functions](https://docs.nvidia.com/index.html#address-space-conversion-functions) -
[10.17. Alloca Function](https://docs.nvidia.com/index.html#alloca-function) -
[10.18. Compiler Optimization Hint Functions](https://docs.nvidia.com/index.html#compiler-optimization-hint-functions) [10.19. Warp Vote Functions](https://docs.nvidia.com/index.html#warp-vote-functions)-
[10.20. Warp Match Functions](https://docs.nvidia.com/index.html#warp-match-functions) -
[10.21. Warp Reduce Functions](https://docs.nvidia.com/index.html#warp-reduce-functions) -
[10.22. Warp Shuffle Functions](https://docs.nvidia.com/index.html#warp-shuffle-functions) -
[10.23. Nanosleep Function](https://docs.nvidia.com/index.html#nanosleep-function) -
[10.24. Warp Matrix Functions](https://docs.nvidia.com/index.html#warp-matrix-functions) -
[10.25. DPX](https://docs.nvidia.com/index.html#dpx) -
[10.26. Asynchronous Barrier](https://docs.nvidia.com/index.html#asynchronous-barrier)[10.26.1. Simple Synchronization Pattern](https://docs.nvidia.com/index.html#simple-synchronization-pattern)[10.26.2. Temporal Splitting and Five Stages of Synchronization](https://docs.nvidia.com/index.html#temporal-splitting-and-five-stages-of-synchronization)[10.26.3. Bootstrap Initialization, Expected Arrival Count, and Participation](https://docs.nvidia.com/index.html#bootstrap-initialization-expected-arrival-count-and-participation)[10.26.4. A Barrierâs Phase: Arrival, Countdown, Completion, and Reset](https://docs.nvidia.com/index.html#a-barrier-s-phase-arrival-countdown-completion-and-reset)[10.26.5. Spatial Partitioning (also known as Warp Specialization)](https://docs.nvidia.com/index.html#spatial-partitioning-also-known-as-warp-specialization)[10.26.6. Early Exit (Dropping out of Participation)](https://docs.nvidia.com/index.html#early-exit-dropping-out-of-participation)[10.26.7. Completion Function](https://docs.nvidia.com/index.html#completion-function)-
[10.26.8. Memory Barrier Primitives Interface](https://docs.nvidia.com/index.html#memory-barrier-primitives-interface)

-
[10.27. Asynchronous Data Copies](https://docs.nvidia.com/index.html#asynchronous-data-copies) -
[10.28. Asynchronous Data Copies using](https://docs.nvidia.com/index.html#asynchronous-data-copies-using-cuda-pipeline)`cuda::pipeline`

-
[10.29. Asynchronous Data Copies using the Tensor Memory Accelerator (TMA)](https://docs.nvidia.com/index.html#asynchronous-data-copies-using-the-tensor-memory-accelerator-tma) -
[10.30. Encoding a Tensor Map on Device](https://docs.nvidia.com/index.html#encoding-a-tensor-map-on-device) [10.31. Profiler Counter Function](https://docs.nvidia.com/index.html#profiler-counter-function)[10.32. Assertion](https://docs.nvidia.com/index.html#assertion)[10.33. Trap function](https://docs.nvidia.com/index.html#trap-function)[10.34. Breakpoint Function](https://docs.nvidia.com/index.html#breakpoint-function)-
[10.35. Formatted Output](https://docs.nvidia.com/index.html#formatted-output) -
[10.36. Dynamic Global Memory Allocation and Operations](https://docs.nvidia.com/index.html#dynamic-global-memory-allocation-and-operations) [10.37. Execution Configuration](https://docs.nvidia.com/index.html#execution-configuration)[10.38. Launch Bounds](https://docs.nvidia.com/index.html#launch-bounds)[10.39. Maximum Number of Registers per Thread](https://docs.nvidia.com/index.html#maximum-number-of-registers-per-thread)[10.40. #pragma unroll](https://docs.nvidia.com/index.html#pragma-unroll)[10.41. SIMD Video Instructions](https://docs.nvidia.com/index.html#simd-video-instructions)[10.42. Diagnostic Pragmas](https://docs.nvidia.com/index.html#diagnostic-pragmas)[10.43. Custom ABI Pragmas](https://docs.nvidia.com/index.html#custom-abi-pragmas)[10.44. CUDA C++ Memory Model](https://docs.nvidia.com/index.html#cuda-c-memory-model)[10.45. CUDA C++ Execution Model](https://docs.nvidia.com/index.html#cuda-c-execution-model)

-
-
[11. Cooperative Groups](https://docs.nvidia.com/index.html#cooperative-groups) -
[12. Cluster Launch Control](https://docs.nvidia.com/index.html#cluster-launch-control) -
[13. CUDA Dynamic Parallelism](https://docs.nvidia.com/index.html#cuda-dynamic-parallelism)-
[13.1. Introduction](https://docs.nvidia.com/index.html#introduction-cuda-dynamic-parallelism) -
[13.2. Execution Environment and Memory Model](https://docs.nvidia.com/index.html#execution-environment-and-memory-model) -
[13.3. Programming Interface](https://docs.nvidia.com/index.html#programming-interface-cdp)-
[13.3.1. CUDA C++ Reference](https://docs.nvidia.com/index.html#cuda-c-reference) -
[13.3.2. Device-side Launch from PTX](https://docs.nvidia.com/index.html#device-side-launch-from-ptx) -
[13.3.3. Toolkit Support for Dynamic Parallelism](https://docs.nvidia.com/index.html#toolkit-support-for-dynamic-parallelism)

-
-
[13.4. Programming Guidelines](https://docs.nvidia.com/index.html#programming-guidelines) -
[13.5. CDP2 vs CDP1](https://docs.nvidia.com/index.html#cdp2-vs-cdp1) -
[13.6. Legacy CUDA Dynamic Parallelism (CDP1)](https://docs.nvidia.com/index.html#legacy-cuda-dynamic-parallelism-cdp1)-
[13.6.1. Execution Environment and Memory Model (CDP1)](https://docs.nvidia.com/index.html#execution-environment-and-memory-model-cdp1) -
[13.6.2. Programming Interface (CDP1)](https://docs.nvidia.com/index.html#programming-interface-cdp1)-
[13.6.2.1. CUDA C++ Reference (CDP1)](https://docs.nvidia.com/index.html#cuda-c-reference-cdp1) -
[13.6.2.2. Device-side Launch from PTX (CDP1)](https://docs.nvidia.com/index.html#device-side-launch-from-ptx-cdp1) -
[13.6.2.3. Toolkit Support for Dynamic Parallelism (CDP1)](https://docs.nvidia.com/index.html#toolkit-support-for-dynamic-parallelism-cdp1)

-
-
[13.6.3. Programming Guidelines (CDP1)](https://docs.nvidia.com/index.html#programming-guidelines-cdp1)[13.6.3.1. Basics (CDP1)](https://docs.nvidia.com/index.html#basics-cdp1)-
[13.6.3.2. Performance (CDP1)](https://docs.nvidia.com/index.html#performance-cdp1) -
[13.6.3.3. Implementation Restrictions and Limitations (CDP1)](https://docs.nvidia.com/index.html#implementation-restrictions-and-limitations-cdp1)-
[13.6.3.3.1. Runtime (CDP1)](https://docs.nvidia.com/index.html#runtime-cdp1)[13.6.3.3.1.1. Memory Footprint (CDP1)](https://docs.nvidia.com/index.html#memory-footprint-cdp1)[13.6.3.3.1.2. Nesting and Synchronization Depth (CDP1)](https://docs.nvidia.com/index.html#nesting-and-synchronization-depth-cdp1)[13.6.3.3.1.3. Pending Kernel Launches (CDP1)](https://docs.nvidia.com/index.html#pending-kernel-launches-cdp1)[13.6.3.3.1.4. Configuration Options (CDP1)](https://docs.nvidia.com/index.html#configuration-options-cdp1)[13.6.3.3.1.5. Memory Allocation and Lifetime (CDP1)](https://docs.nvidia.com/index.html#memory-allocation-and-lifetime-cdp1)[13.6.3.3.1.6. SM Id and Warp Id (CDP1)](https://docs.nvidia.com/index.html#sm-id-and-warp-id-cdp1)[13.6.3.3.1.7. ECC Errors (CDP1)](https://docs.nvidia.com/index.html#ecc-errors-cdp1)

-

-

-
-
[14. Virtual Memory Management](https://docs.nvidia.com/index.html#virtual-memory-management) -
[15. Stream Ordered Memory Allocator](https://docs.nvidia.com/index.html#stream-ordered-memory-allocator)[15.1. Introduction](https://docs.nvidia.com/index.html#stream-ordered-memory-allocator-intro)[15.2. Query for Support](https://docs.nvidia.com/index.html#stream-ordered-querying-memory-support)[15.3. API Fundamentals (cudaMallocAsync and cudaFreeAsync)](https://docs.nvidia.com/index.html#api-fundamentals-cudamallocasync-and-cudafreeasync)[15.4. Memory Pools and the cudaMemPool_t](https://docs.nvidia.com/index.html#memory-pools-and-the-cudamempool-t)[15.5. Default/Implicit Pools](https://docs.nvidia.com/index.html#default-implicit-pools)[15.6. Explicit Pools](https://docs.nvidia.com/index.html#explicit-pools)[15.7. Physical Page Caching Behavior](https://docs.nvidia.com/index.html#physical-page-caching-behavior)[15.8. Resource Usage Statistics](https://docs.nvidia.com/index.html#resource-usage-statistics)-
[15.9. Memory Reuse Policies](https://docs.nvidia.com/index.html#memory-reuse-policies) [15.10. Device Accessibility for Multi-GPU Support](https://docs.nvidia.com/index.html#device-accessibility-for-multi-gpu-support)-
[15.11. IPC Memory Pools](https://docs.nvidia.com/index.html#ipc-memory-pools) [15.12. Synchronization API Actions](https://docs.nvidia.com/index.html#synchronization-api-actions)-
[15.13. Addendums](https://docs.nvidia.com/index.html#addendums)

-
[16. Graph Memory Nodes](https://docs.nvidia.com/index.html#graph-memory-nodes) -
[17. Mathematical Functions](https://docs.nvidia.com/index.html#mathematical-functions-appendix) -
[18. C++ Language Support](https://docs.nvidia.com/index.html#c-language-support)[18.1. C++11 Language Features](https://docs.nvidia.com/index.html#c-11-language-features)[18.2. C++14 Language Features](https://docs.nvidia.com/index.html#c-14-language-features)[18.3. C++17 Language Features](https://docs.nvidia.com/index.html#c-17-language-features)[18.4. C++20 Language Features](https://docs.nvidia.com/index.html#c-20-language-features)-
[18.5. Restrictions](https://docs.nvidia.com/index.html#language-restrictions)[18.5.1. Host Compiler Extensions](https://docs.nvidia.com/index.html#host-compiler-extensions)-
[18.5.2. Preprocessor Symbols](https://docs.nvidia.com/index.html#preprocessor-symbols) -
[18.5.3. Qualifiers](https://docs.nvidia.com/index.html#qualifiers) [18.5.4. Pointers](https://docs.nvidia.com/index.html#pointers)-
[18.5.5. Operators](https://docs.nvidia.com/index.html#operators) [18.5.6. Run Time Type Information (RTTI)](https://docs.nvidia.com/index.html#run-time-type-information-rtti)[18.5.7. Exception Handling](https://docs.nvidia.com/index.html#exception-handling)[18.5.8. Standard Library](https://docs.nvidia.com/index.html#standard-library)[18.5.9. Namespace Reservations](https://docs.nvidia.com/index.html#namespace-reservations)-
[18.5.10. Functions](https://docs.nvidia.com/index.html#functions)[18.5.10.1. External Linkage](https://docs.nvidia.com/index.html#external-linkage)[18.5.10.2. Implicitly-declared and non-virtual explicitly-defaulted functions](https://docs.nvidia.com/index.html#implicitly-declared-and-non-virtual-explicitly-defaulted-functions)-
[18.5.10.3. Function Parameters](https://docs.nvidia.com/index.html#function-parameters) [18.5.10.4. Static Variables within Function](https://docs.nvidia.com/index.html#static-variables-within-function)[18.5.10.5. Function Pointers](https://docs.nvidia.com/index.html#function-pointers)[18.5.10.6. Function Recursion](https://docs.nvidia.com/index.html#function-recursion)[18.5.10.7. Friend Functions](https://docs.nvidia.com/index.html#friend-functions)[18.5.10.8. Operator Function](https://docs.nvidia.com/index.html#operator-function)[18.5.10.9. Allocation and Deallocation Functions](https://docs.nvidia.com/index.html#allocation-and-deallocation-functions)

-
[18.5.11. Classes](https://docs.nvidia.com/index.html#classes) [18.5.12. Templates](https://docs.nvidia.com/index.html#templates)[18.5.13. Trigraphs and Digraphs](https://docs.nvidia.com/index.html#trigraphs-and-digraphs)[18.5.14. Const-qualified variables](https://docs.nvidia.com/index.html#const-qualified-variables)[18.5.15. Long Double](https://docs.nvidia.com/index.html#long-double)[18.5.16. Deprecation Annotation](https://docs.nvidia.com/index.html#deprecation-annotation)[18.5.17. Noreturn Annotation](https://docs.nvidia.com/index.html#noreturn-annotation)[18.5.18. [[likely]] / [[unlikely]] Standard Attributes](https://docs.nvidia.com/index.html#likely-unlikely-standard-attributes)[18.5.19. const and pure GNU Attributes](https://docs.nvidia.com/index.html#const-and-pure-gnu-attributes)[18.5.20. __nv_pure__ Attribute](https://docs.nvidia.com/index.html#nv-pure-attribute)[18.5.21. Intel Host Compiler Specific](https://docs.nvidia.com/index.html#intel-host-compiler-specific)-
[18.5.22. C++11 Features](https://docs.nvidia.com/index.html#c-11-features)[18.5.22.1. Lambda Expressions](https://docs.nvidia.com/index.html#lambda-expressions)[18.5.22.2. std::initializer_list](https://docs.nvidia.com/index.html#std-initializer-list)[18.5.22.3. Rvalue references](https://docs.nvidia.com/index.html#rvalue-references)[18.5.22.4. Constexpr functions and function templates](https://docs.nvidia.com/index.html#constexpr-functions-and-function-templates)[18.5.22.5. Constexpr variables](https://docs.nvidia.com/index.html#constexpr-variables)-
[18.5.22.6. Inline namespaces](https://docs.nvidia.com/index.html#inline-namespaces) [18.5.22.7. thread_local](https://docs.nvidia.com/index.html#thread-local)[18.5.22.8. __global__ functions and function templates](https://docs.nvidia.com/index.html#global-functions-and-function-templates)[18.5.22.9. __managed__ and __shared__ variables](https://docs.nvidia.com/index.html#managed-and-shared-variables)[18.5.22.10. Defaulted functions](https://docs.nvidia.com/index.html#defaulted-functions)

-
[18.5.23. C++14 Features](https://docs.nvidia.com/index.html#c-14-features) -
[18.5.24. C++17 Features](https://docs.nvidia.com/index.html#c-17-features) -
[18.5.25. C++20 Features](https://docs.nvidia.com/index.html#c-20-features)

[18.6. Polymorphic Function Wrappers](https://docs.nvidia.com/index.html#polymorphic-function-wrappers)-
[18.7. Extended Lambdas](https://docs.nvidia.com/index.html#extended-lambdas) [18.8. Relaxed Constexpr (-expt-relaxed-constexpr)](https://docs.nvidia.com/index.html#relaxed-constexpr-expt-relaxed-constexpr)-
[18.9. Code Samples](https://docs.nvidia.com/index.html#code-samples)

-
[19. Texture Fetching](https://docs.nvidia.com/index.html#texture-fetching) -
[20. Compute Capabilities](https://docs.nvidia.com/index.html#compute-capabilities)-
[20.1. Feature Availability](https://docs.nvidia.com/index.html#feature-availability) [20.2. Features and Technical Specifications](https://docs.nvidia.com/index.html#features-and-technical-specifications)[20.3. Floating-Point Standard](https://docs.nvidia.com/index.html#floating-point-standard)-
[20.4. Compute Capability 5.x](https://docs.nvidia.com/index.html#compute-capability-5-x) -
[20.5. Compute Capability 6.x](https://docs.nvidia.com/index.html#compute-capability-6-x) -
[20.6. Compute Capability 7.x](https://docs.nvidia.com/index.html#compute-capability-7-x) -
[20.7. Compute Capability 8.x](https://docs.nvidia.com/index.html#compute-capability-8-x) -
[20.8. Compute Capability 9.0](https://docs.nvidia.com/index.html#compute-capability-9-0) -
[20.9. Compute Capability 10.0](https://docs.nvidia.com/index.html#compute-capability-10-0) -
[20.10. Compute Capability 12.0](https://docs.nvidia.com/index.html#compute-capability-12-0)

-
-
[21. Driver API](https://docs.nvidia.com/index.html#driver-api)[21.1. Context](https://docs.nvidia.com/index.html#context)[21.2. Module](https://docs.nvidia.com/index.html#module)[21.3. Kernel Execution](https://docs.nvidia.com/index.html#kernel-execution)[21.4. Interoperability between Runtime and Driver APIs](https://docs.nvidia.com/index.html#interoperability-between-runtime-and-driver-apis)-
[21.5. Driver Entry Point Access](https://docs.nvidia.com/index.html#driver-entry-point-access)

[22. CUDA Environment Variables](https://docs.nvidia.com/index.html#cuda-environment-variables)-
[23. Error Log Management](https://docs.nvidia.com/index.html#error-log-management) -
[24. Unified Memory Programming](https://docs.nvidia.com/index.html#unified-memory-programming)-
[24.1. Unified Memory Introduction](https://docs.nvidia.com/index.html#unified-memory-introduction)[24.1.1. System Requirements for Unified Memory](https://docs.nvidia.com/index.html#system-requirements-for-unified-memory)-
[24.1.2. Programming Model](https://docs.nvidia.com/index.html#um-opt-in)[24.1.2.1. Allocation APIs for System-Allocated Memory](https://docs.nvidia.com/index.html#allocation-apis-for-system-allocated-memory)[24.1.2.2. Allocation API for CUDA Managed Memory:](https://docs.nvidia.com/index.html#allocation-api-for-cuda-managed-memory-cudamallocmanaged)`cudaMallocManaged()`

[24.1.2.3. Global-Scope Managed Variables Using](https://docs.nvidia.com/index.html#global-scope-managed-variables-using-managed)`__managed__`

[24.1.2.4. Difference between Unified Memory and Mapped Memory](https://docs.nvidia.com/index.html#difference-between-unified-memory-and-mapped-memory)[24.1.2.5. Pointer Attributes](https://docs.nvidia.com/index.html#um-pointer-attributes)[24.1.2.6. Runtime detection of Unified Memory Support Level](https://docs.nvidia.com/index.html#runtime-detection-of-unified-memory-support-level)[24.1.2.7. GPU Memory Oversubscription](https://docs.nvidia.com/index.html#gpu-memory-oversubscription)-
[24.1.2.8. Performance Hints](https://docs.nvidia.com/index.html#performance-hints)

-
[24.2. Unified memory on devices with full CUDA Unified Memory support](https://docs.nvidia.com/index.html#unified-memory-on-devices-with-full-cuda-unified-memory-support)-
[24.2.1. System-Allocated Memory: in-depth examples](https://docs.nvidia.com/index.html#system-allocated-memory-in-depth-examples) -
[24.2.2. Performance Tuning](https://docs.nvidia.com/index.html#performance-tuning)

-
-
[24.3. Unified memory on devices without full CUDA Unified Memory support](https://docs.nvidia.com/index.html#unified-memory-on-devices-without-full-cuda-unified-memory-support)[24.3.1. Unified memory on devices with only CUDA Managed Memory support](https://docs.nvidia.com/index.html#unified-memory-on-devices-with-only-cuda-managed-memory-support)-
[24.3.2. Unified memory on Windows or devices with compute capability 5.x](https://docs.nvidia.com/index.html#unified-memory-on-windows-or-devices-with-compute-capability-5-x)[24.3.2.1. Data Migration and Coherency](https://docs.nvidia.com/index.html#data-migration-and-coherency)[24.3.2.2. GPU Memory Oversubscription](https://docs.nvidia.com/index.html#um-legacy-oversubscription)[24.3.2.3. Multi-GPU](https://docs.nvidia.com/index.html#multi-gpu)-
[24.3.2.4. Coherency and Concurrency](https://docs.nvidia.com/index.html#coherency-and-concurrency)[24.3.2.4.1. GPU Exclusive Access To Managed Memory](https://docs.nvidia.com/index.html#gpu-exclusive-access-to-managed-memory)[24.3.2.4.2. Explicit Synchronization and Logical GPU Activity](https://docs.nvidia.com/index.html#explicit-synchronization-and-logical-gpu-activity)[24.3.2.4.3. Managing Data Visibility and Concurrent CPU + GPU Access with Streams](https://docs.nvidia.com/index.html#managing-data-visibility-and-concurrent-cpu-gpu-access-with-streams)[24.3.2.4.4. Stream Association Examples](https://docs.nvidia.com/index.html#stream-association-examples)[24.3.2.4.5. Stream Attach With Multithreaded Host Programs](https://docs.nvidia.com/index.html#stream-attach-with-multithreaded-host-programs)[24.3.2.4.6. Advanced Topic: Modular Programs and Data Access Constraints](https://docs.nvidia.com/index.html#advanced-topic-modular-programs-and-data-access-constraints)[24.3.2.4.7. Memcpy()/Memset() Behavior With Stream-associated Unified Memory](https://docs.nvidia.com/index.html#memcpy-memset-behavior-with-stream-associated-unified-memory)

-
-
[25. Lazy Loading](https://docs.nvidia.com/index.html#lazy-loading) -
[26. Extended GPU Memory](https://docs.nvidia.com/index.html#extended-gpu-memory) -
[27. Notices](https://docs.nvidia.com/index.html#notices)
