# ⚙️ Operating Systems — Interview Questions & Answers

> Quick-reference guide for the most frequently asked OS questions in product-based company interviews.

---

## 1. Introduction to OS

### Q1. OS and its Main Functions

An **Operating System** is software that manages hardware and software resources, acting as an intermediary between users and hardware.

**Main Functions:** Process management, Memory management, File management, I/O management, Security, Networking.

---

### Q2. Types of OS

| Type                  | Description                                           | Example          |
| --------------------- | ----------------------------------------------------- | ---------------- |
| **Batch OS**          | Jobs processed in batches without interaction         | Early mainframes |
| **Multi-programming** | Multiple programs in memory; CPU switches on I/O wait |                  |
| **Multi-tasking**     | CPU time-shares between tasks                         | Windows, Linux   |
| **Real-Time OS**      | Strict time constraints                               | RTOS, VxWorks    |
| **Distributed OS**    | Multiple machines as one system                       | Google's systems |

---

### Q3. Batch OS

Jobs collected and processed in groups without user interaction. Pros: efficient for repetitive tasks. Cons: no interactivity, hard to debug.

---

### Q4. Multiprogramming and Multitasking OS

- **Multiprogramming:** Keep CPU busy by loading multiple programs; switch when one waits for I/O.
- **Multitasking:** Multiprogramming + time-sharing; each process gets a time quantum.

---

### Q5. Kernel and User Modes

- **Kernel Mode:** Full hardware access, privileged instructions (OS runs here)
- **User Mode:** Restricted access (applications run here)
- **System call** switches from User → Kernel mode

**Kernel Types:** Monolithic (Linux), Microkernel (Minix), Hybrid (Windows, macOS)

---

### Q6. Process and its States

A **process** is a program in execution.

**States:** New → Ready → Running → Terminated (with Waiting/Blocked as a side state)

**PCB (Process Control Block):** Stores PID, state, registers, memory info, priority.

---

### Q7. Normal Function Call vs System Calls

- **Function Call:** Within user space, fast, no mode switch (`printf()`)
- **System Call:** User → Kernel space, slower, mode switch (`fork()`, `read()`, `open()`)

**Types:** Process control, File management, Device management, Communication, Information.

---

## 2. Process Management

### Q8. Starvation and Aging

- **Starvation:** Process waits indefinitely as higher-priority processes keep getting CPU.
- **Aging:** Fix — gradually increase priority of waiting processes over time.

---

### Q9. Process Synchronization and its Tools

Ensures multiple processes access shared resources without conflicts.

**Critical Section Requirements:** Mutual Exclusion, Progress, Bounded Waiting.

**Tools:** Mutex, Semaphores, Monitors, Spinlocks, Peterson's Solution.

---

### Q10. Semaphores and Types

Integer variable for process synchronization.

| Type         | Values | Use                       |
| ------------ | ------ | ------------------------- |
| **Binary**   | 0 or 1 | Mutual exclusion          |
| **Counting** | 0 to N | N instances of a resource |

**Operations:** `wait(S)` / P() decrements; `signal(S)` / V() increments.

---

### Q11. Deadlock and Prevention

**Deadlock:** Two+ processes waiting for each other; none can proceed.

**Four Necessary Conditions:** Mutual Exclusion, Hold & Wait, No Preemption, Circular Wait.

**Prevention:** Break any condition. **Avoidance:** Banker's Algorithm. **Detection:** RAG. **Recovery:** Kill processes or preempt resources.

---

### Q12. Banker's Algorithm

Deadlock avoidance — checks if granting a request leads to a safe state.

**Matrices:** Available, Max, Allocation, Need (= Max - Allocation).
**Safe State:** A sequence exists where all processes can finish.

---

## 3. Memory Management

### Q13. Memory Management Techniques

| Strategy      | How                      | Pros           | Cons                   |
| ------------- | ------------------------ | -------------- | ---------------------- |
| **First Fit** | First hole large enough  | Fast           | External fragmentation |
| **Best Fit**  | Smallest sufficient hole | Least waste    | Slow; tiny fragments   |
| **Worst Fit** | Largest hole             | Large leftover | Worst fragmentation    |

---

### Q14. Virtual Memory

Uses disk as RAM extension. Only needed pages loaded (**demand paging**). Processes use virtual addresses mapped to physical addresses by **MMU**.

**Benefits:** Run programs larger than RAM, process isolation, efficient memory use.

---

### Q15. Dynamic Binding

Binding process to physical memory at **runtime** (not compile/load time). Most flexible; allows relocation. Requires MMU hardware support.

---

### Q16. Page Fault

Process accesses page not in RAM → OS trap → load page from disk → update page table → resume. If no free frame → **page replacement** (FIFO, LRU, Optimal).

---

### Q17. Belady's Anomaly

More frames → MORE page faults (counterintuitive). Only in **FIFO**. Does NOT occur in LRU or Optimal (stack algorithms).

---

### Q18. Thrashing

Process spends more time swapping pages than executing. Cause: too many processes, not enough frames.

**Solutions:** Working Set Model, Page Fault Frequency control, reduce multiprogramming.

---

### Q19. Cache

Small, fast memory between CPU and RAM.

| Level  | Speed    | Size         |
| ------ | -------- | ------------ |
| **L1** | Fastest  | ~64 KB       |
| **L2** | Fast     | ~256 KB–1 MB |
| **L3** | Moderate | ~8–32 MB     |

**Locality:** Temporal (recent data reused) and Spatial (nearby data accessed).

---

### Q20. Direct and Associative Mapping

| Mapping               | How                         | Trade-off                    |
| --------------------- | --------------------------- | ---------------------------- |
| **Direct**            | Block → specific cache line | Fast lookup, conflict misses |
| **Fully Associative** | Block → any line            | No conflicts, slow search    |
| **Set-Associative**   | Block → set of N lines      | Balanced                     |

---

## 4. File Systems

### Q21. File System and Components

Organizes data storage and retrieval. Components: Files, Directories, Metadata, FCB (File Control Block), Storage blocks.

---

### Q22. Types of File Systems

**FAT32** (simple, 4GB limit), **NTFS** (journaling, Windows), **ext4** (Linux), **APFS** (macOS, SSD-optimized), **XFS** (high-performance Linux).

---

### Q23. File Allocation and Deallocation

| Method         | How                           | Trade-off                            |
| -------------- | ----------------------------- | ------------------------------------ |
| **Contiguous** | Consecutive blocks            | Fast access, external fragmentation  |
| **Linked**     | Blocks linked via pointers    | No fragmentation, slow random access |
| **Indexed**    | Index block with all pointers | Fast access, index overhead          |

---

### Q24. Fragmentation

- **Internal:** Allocated block > needed (wasted space inside). Solution: smaller page sizes.
- **External:** Free memory not contiguous. Solution: compaction, paging.

---

## 5. I/O Systems

### Q25. Blocking vs. Non-Blocking I/O

- **Blocking:** Process waits until I/O completes (simple, CPU idle)
- **Non-Blocking:** Process continues; checks later (complex, CPU efficient)

---

### Q26. Synchronous vs. Asynchronous I/O

- **Synchronous:** Returns after I/O done (waits)
- **Asynchronous:** Returns immediately; notified via callback/signal

---

### Q27. Spooling

**SPOOL** = Simultaneous Peripheral Operations On-Line. Buffer holds data for slow devices (e.g., print queue). CPU freed for other work.

---

## 6. Storage Management and Data Protection

### Q28. Security Threats and Vulnerabilities

**Threats:** Virus, Worm, Trojan, Ransomware, Rootkit, Spyware.

**Protection:** Authentication (MFA), Access Control (RBAC), Encryption, Firewalls, Antivirus, Auditing.

---

> 📖 **Source:** [TakeUForward — Most Asked OS Interview Questions](https://takeuforward.org/operating-system/most-asked-operating-system-interview-questions)
