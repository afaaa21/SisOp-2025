# Rangkuman Appendix A: Influential Operating Systems

**Nama**: Afriq Fadili Azim  
**NRP**: 3124500043  
**Dosen Pengajar**: Dr Ferry Astika Saputra ST, M.Sc

## 1. Background and Feature Migration

### A. Core Theme  
Features developed for mainframes migrated to smaller systems as technology advanced:  
- **Spooling** (from MULTICS) → Adapted for I/O efficiency in PCs.  
- **Virtual Memory** (pioneered in Atlas) → Standard for dynamic memory management.  
- **Time-Sharing** (CTSS) → Inspired interactive OS like UNIX and Windows.  

### B. Purpose of Study  
Understanding OS history reveals patterns of innovation and adaptation (e.g., multiprocessing, microkernel designs).  


## 2. Early Computing Era (1940s–1950s)

### A. Manchester Mark 1 (1949) & Ferranti Mark 1 (1951)  
- **First stored-program computers**.  
- Manual operation via consoles (punch cards, switches).  
- Debugging via console indicator lights.  

### B. Limitations  
- Frequent CPU idle time due to setup delays.  
- High operational costs.  


## 3. Evolution to Batch Systems and Automation

### A. Dedicated Systems  
- Device drivers for I/O management.  
- Emergence of FORTRAN/COBOL increased complexity.  

### B. Batch Processing  
- **Professional operators** replaced programmers.  
- **Resident Monitor**: Automated job sequencing via control cards (e.g., `$JOB`, `$RUN`).  
- Example: IBM OS/360’s Job Control Language (JCL).  

### C. Spooling (1960s)  
- Disks as buffers for overlapping I/O and computation.  
- Example: MULTICS used spooling for parallel I/O.  

### D. Overlapped I/O  
- Shift from tapes (sequential) to disks (random-access).  


## 4. Key Operating Systems and Their Innovations

### A. Atlas (1950s–1960s)  
- **Innovations**:  
  - Demand paging (drum ↔ core memory).  
  - Page replacement algorithm (history-based prediction: `t₁`, `t₂`).  
  - Spooling for CPU optimization.  
- **Architecture**:  
  - 16 KB core + 98 KB drum.  
  - 512-word pages with associative memory.  

### B. XDS-940 (1960s)  
- First time-sharing system with **paging for relocation**.  
- Swapped processes (64 KB physical memory).  
- Introduced user/monitor modes.  

### C. THE OS (Technische Hogeschool Eindhoven)  
- **Layered design** (memory management → user interface).  
- **Semaphores** for process synchronization.  
- **Banker’s Algorithm** for deadlock prevention.  
- **Software paging** via Algol compiler.  

### D. RC 4000 (1960s)  
- **Modular kernel** with message-passing IPC.  
- Atomic operations: `send-message`, `wait-message`.  
- Treated I/O devices as processes.  

### E. CTSS (1961) & MULTICS (1965–1970)  
- **CTSS (MIT)**:  
  - First experimental time-sharing (32 users).  
  - Multilevel feedback queue scheduling.  
- **MULTICS**:  
  - Segmented-paged memory + hierarchical file system.  
  - Security via access lists and protection rings.  
  - Inspired UNIX despite commercial failure.  

### F. IBM OS/360 (1960s)  
- **Goal**: Single OS for IBM/360 family.  
- **Issues**:  
  - High overhead (assembly code).  
  - Rigid file system (predefined sizes).  
- **Legacy**: OS/VS (virtual memory), TSO (Time-Sharing Option).  

### G. Mach (1980s)  
- **Microkernel design**:  
  - Separated core functions (scheduling, messaging).  
  - Message-passing with virtual memory optimization.  
- Foundation for macOS (XNU) and GNU HURD.  

### H. CP/M & MS-DOS (1970s–1980s)  
- **CP/M**: Dominant 8-bit OS (Intel 8080).  
- **MS-DOS**:  
  - Built for IBM PCs (8086).  
  - Limited memory protection → crash-prone.  

### I. GUI-Based Systems (1980s–Present)  
- **Macintosh OS (1984)**:  
  - First consumer-friendly GUI + mouse support.  
  - Hierarchical file system.  
- **Windows**:  
  - Licensed to multiple vendors.  
  - Evolved from 16-bit (Windows 1.0) to 64-bit (Windows 11).  

### J. Capability-Based Systems: Hydra & CAP  
- **Hydra**:  
  - Rights amplification for trusted procedures.  
- **CAP (Cambridge)**:  
  - Hardware + software capabilities.  
  - Security via `seal/unseal` mechanisms.  

---

## 5. Other Influential Systems  
- **MCP (Burroughs)**: First OS in a system programming language.  
- **SCOPE (CDC 6600)**: Advanced multi-CPU synchronization.  
- **VM/CP (IBM)**: Virtualization for CMS.  

---

## 6. Lessons and Legacy  
- **Feature Migration**: Virtual memory, GUIs, multithreading → mainstream.  
- **Modular Design**: Layered architectures (THE OS), microkernels (Mach).  
- **Failures as Inspiration**: MULTICS → UNIX; TSS/360 → modern systems.  
