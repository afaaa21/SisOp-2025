# Tugas Week 2

**Nama**: Afriq Fadili Azim  
**NRP**: 3124500043  
**Dosen Pengajar**: Dr Ferry Astika Saputra ST, M.Sc  

---

### 1. What are the three main purposes of an operating system?  
a. **Manage computer hardware**: The operating system acts as an intermediary between hardware and application programs, managing resources such as the CPU, memory, and I/O devices.  
b. **Provide an environment for application programs to run**: The operating system provides interfaces and services that allow application programs to run efficiently.  
c. **Act as a resource allocator**: The operating system allocates resources such as CPU time, memory, and storage space to various programs and users.  

---

### 2. When is it appropriate for the operating system to forsake efficiency to "waste" resources? Why is such a system not really wasteful?  
The operating system may "waste" resources for:  
a. **Security**: E.g., using more memory for process isolation or data encryption.  
b. **User convenience**: E.g., allocating resources for a responsive user interface.  
c. **Redundancy**: E.g., creating redundant backups for high availability.  

This is not truly wasteful because it improves reliability, security, or user experience, providing greater overall value.  

---

### 3. What is the main difficulty in writing an OS for a real-time environment?  
The main difficulty is ensuring **strict timing constraints** (hard real-time constraints). The system must respond within specified time limits; failure can result in system failure.  

---

### 4. Should the OS include applications like web browsers and mail programs?  
**Arguments for inclusion**:  
- **User convenience**: No need to install additional apps.  
- **Better integration**: Integrated apps work more efficiently with system resources.  

**Arguments against inclusion**:  
- **OS size**: Increases OS size, unsuitable for devices with limited space.  
- **User freedom**: Users may prefer third-party apps.  

---

### 5. How does kernel mode vs. user mode function as protection?  
**Kernel mode** restricts access to critical instructions and resources. Only kernel-mode code can execute privileged operations (e.g., I/O access, system settings). This prevents user programs from interfering with system operations.  

---

### 6. Which instructions should be privileged?  
Privileged instructions:  
- Set value of timer  
- Clear memory  
- Turn off interrupts  
- Modify entries in device-status table  
- Switch from user to kernel mode  
- Access I/O device  

**Reason**: These directly affect system operations and can cause damage if misused.  

---

### 7. Two difficulties with placing the OS in a non-modifiable memory partition:  
a. **Limited flexibility**: The OS cannot modify itself to fix bugs or enhance functionality.  
b. **Memory management challenges**: Dynamic memory management becomes difficult if the OS cannot adjust its partition.  

---

### 8. Two uses of multiple CPU modes:  
1. **Virtualization**: A dedicated mode for the virtual machine manager (VMM) to run multiple OSes.  
2. **Enhanced security**: Stricter isolation between processes or services.  

---

### 9. How timers compute current time:  
a. Count timer ticks since system boot.  
b. Multiply ticks by the time interval per tick.  
c. Add the result to the boot time.  

---

### 10. Why are caches useful?  
**Usefulness**:  
- **Increase access speed**: Store frequently accessed data.  
- **Reduce CPU load**: Minimize repeated access to slower storage.  

**Problems solved**:  
- Reduce latency.  
- Improve performance.  

**Problems caused**:  
- Cache coherence issues.  
- Management overhead.  

**Why not replace devices with large caches?**: Caches are volatile; data is lost on power-off. Devices (e.g., disks) provide permanent storage.  

---

### 11. Client-Server vs. Peer-to-Peer Models:  
**Client-Server**:  
- Clear separation between clients (requesters) and servers (providers).  
- Centralized servers may become bottlenecks.  
- Example: Web servers, databases.  

**Peer-to-Peer (P2P)**:  
- Nodes act as both clients and servers.  
- Decentralized, fault-tolerant.  
- Example: BitTorrent, Skype.  
