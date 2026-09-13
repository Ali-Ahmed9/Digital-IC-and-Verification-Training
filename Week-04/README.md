# Week 04: Cache Memories & Memory Hierarchy
**Course:** Advanced Embedded Systems (EE-5043)  
**Reference Text:** *Computer Organization and Design* by Patterson & Hennessy (Chapter 5)

======================================================

## 📖 Overview
This week covers the fundamental principles of memory hierarchy, the organization of cache memory, data placement strategies, replacement policies, and techniques to improve cache performance.

======================================================


## 1. The Memory Wall & Hierarchy
*   **The Problem:** The growing disparity between CPU speed (growing ~50% per year) and DRAM speed creates a "Memory Wall" / "Bandwidth Wall."
*   **The Solution:** A memory hierarchy. Fast, small, expensive memory (Registers, L1) sits near the CPU, while slow, large, cheap memory (Disk, Main Memory) sits further away.
*   **Key Principle:** **Locality of Reference**.
    *   **Temporal Locality:** If a location is referenced once, it is likely to be referenced again soon (e.g., loops).
    *   **Spatial Locality:** If a location is referenced, nearby locations are likely to be referenced soon (e.g., arrays).

### Terminology

| Term             |             Definition |

| **Hit**          |             Data is found in the current cache level. |
| **Miss**         |             Data is not found; must retrieve from lower level. |
| **Hit Rate**     |             Fraction of accesses found in cache (Hits / Total Accesses). |
| **Miss Rate**    |             1 - Hit Rate. |
| **Miss Penalty** |             Time to replace a block in upper level + Time to deliver to processor. |
| **Valid Bit**    |             Indicates if the cache slot holds valid program data. |
| **Dirty Bit**    |             Indicates if a line has been modified in cache (needs write-back). |

======================================================


## 2. Cache Organization & Data Placement
The cache views a memory address as: **`[ Tag | Index/Set | Offset ]`**

There are three primary mapping schemes:

### A. Direct-Mapped Cache
*   **Mapping:** Each block maps to exactly **one** cache line.
*   **Formula:** `Set = Block Number MOD Number of Sets`
*   **Pros:** Simple, fast, lowest power.
*   **Cons:** High **Conflict Misses** (thrashing) if multiple blocks map to the same line.
*   **Example (16KB Cache, 32B Line):** 512 lines, 9 Set bits, 5 Offset bits, 18 Tag bits.

### B. Fully Associative Cache
*   **Mapping:** A block can go **anywhere** in the cache.
*   **Lookup:** All tags compared in parallel (needs a comparator per line).
*   **Pros:** Zero Conflict Misses.
*   **Cons:** Expensive hardware, complex replacement policy.

### C. Set-Associative Cache (N-Way)
*   **Mapping:** A compromise. Each block maps to a specific *set*, but can be placed in any of the *N ways* (lines) within that set.
*   **Example (2-Way):** 16KB Cache, 32B Line -> 256 Sets, 2 ways per set. 8 Set bits, 5 Offset bits, 19 Tag bits.
*   **Rule of Thumb (2:1 Cache Rule):** A 1-way associative cache of size X has roughly the same miss rate as a 2-way associative cache of size X/2.

======================================================


## 3. Cache Replacement Policies
When a miss occurs and the set is full, a block must be evicted.

*   **Optimal:** Replace the block not needed for the longest time. *Best, but unrealistic (requires future knowledge).*
*   **Random:** Randomly select a block. *Surprisingly effective, simple.*
*   **FIFO (First-In-First-Out):** Replace the oldest block. *Not consistent with LRU.*
*   **LRU (Least Recently Used):** Replace the block unused for the longest time. *Good for Temporal Locality, but expensive to implement for high associativity.*
*   **LFU (Least Frequently Used):** Replace the block used the least number of times.
*   **Pseudo-LRU (Tree-based):** An approximation of LRU using a tree of bits (0 = Left, 1 = Right) to track MRU blocks. Cheaper than true LRU.

======================================================

## 4. Write Strategies
What happens when the CPU writes data?

*   **Write-Through:**
    *   Write to **both** Cache and Main Memory.
    *   *Pros:* Easy to implement, read misses never result in writes.
    *   *Cons:* High memory traffic (slows down).
    *   *Solution:* Use a **Write Buffer** (FIFO) to let the CPU continue while memory updates in the background.
*   **Write-Back:**
    *   Write **only** to Cache. Main memory is updated only when the dirty block is evicted.
    *   *Pros:* Less memory traffic (good for repeated writes).
    *   *Cons:* Complex, requires Dirty Bit.
*   **Write Miss Policies:**
    *   **Write Allocate:** Fetch the line into cache, then update it (goes with Write-Back).
    *   **Write No-Allocate:** Do not fetch the line; update directly in memory (goes with Write-Through).

======================================================


## 5. Improving Cache Performance

### A. Reduce Miss Rate
*   **Increase Associativity:** Reduces conflict misses.
*   **Victim Cache:** A small, fully associative cache that holds recently evicted lines. Gives evicted lines a "second chance" before going to memory.
*   **Stream Buffers:** For scanning large arrays (where data is used once), put new lines into a stream buffer instead of the cache to avoid thrashing the cache.
*   **Compiler Optimizations:**
    *   **Loop Interchange:** Change loop nesting to access memory sequentially (improves spatial locality).
    *   **Loop Fusion:** Combine two independent loops into one (reduces loop overhead, improves temporal locality).
    *   **Merge Arrays:** Merge two arrays into one array of structs (improves spatial locality).

### B. Reduce Miss Penalty
*   **Critical Word First / Early Restart:** Send the requested word to the CPU immediately, don't wait for the full block to load.
*   **Non-Blocking Caches (Hit under Miss / Miss under Miss):** Allow the CPU to continue executing other instructions while a miss is being handled.
*   **Multilevel Caches (L1, L2, L3):** L1 is small and fast (focus on Hit Time). L2 is larger and slower (focus on Miss Penalty).

### C. Reduce Hit Time
*   Keep L1 cache small and simple.
*   Use Virtual Memory / TLB to speed up address translation.

======================================================

## 6. The "3 Cs" of Cache Misses
1.  **Compulsory (Cold):** First access to a block. (Unavoidable).
2.  **Capacity:** Cache cannot contain all blocks needed. (Solution: Increase cache size).
3.  **Conflict (Collision):** Multiple blocks map to the same cache line. (Solution: Increase associativity or cache size).
4.  **Coherence (Invalidation):** Another processor/I/O device updates memory. (Solution: Snooping protocols).

### Design Trade-offs (At Constant Cost)
| Cache Type            | Size   | Compulsory Miss | Conflict Miss | Capacity Miss |

| **Direct Mapped**     | Big    | Same            | High          | Low           |
| **N-Way Set Assoc**   | Medium | Same            | Medium        | Medium        |
| **Fully Associative** | Small  | Same            | Zero          | High          |

======================================================


## 📝 Key Formulas
    `AMAT = Hit Time + (Miss Rate × Miss Penalty)`
*   **Effective Access Time:**
    `t_effective = (t_cache × Hit Rate) + (t_mem × (1 - Hit Rate))`
