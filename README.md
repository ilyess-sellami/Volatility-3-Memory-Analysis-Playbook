# Volatility 3 Memory Analysis Playbook

This playbook standardizes the analysis of memory dumps using **[Volatility 3](https://github.com/volatilityfoundation/volatility3)** to:

- Identify **malicious processes**
- Detect **persistence mechanisms**
- Extract **network indicators (C2, sockets, connections)**
- Reconstruct **attacker behavior** from volatile memory
- Correlate **memory artifacts with incident timeline**

This playbook is not just a set of commands. It's a **question-driven investigation framework** designed to help you think like a senior DFIR analyst during memory analysis.

---

## 00 - Evidence Integrity & Hash Verification

### What is the SHA256/MD5 hash of the memory dump?

```bash
sha256sum memory.raw
md5sum memory.raw
```

### What is the size of the memory dump?

```bash
ls -lh memory.raw
```

---

## 01 - Memory Image Identification & System Context

### What operating system is running?

```bash
vol -f memory.raw banners
```

### What is the Windows system information (hostname, build version, timezone, process architecture)?

```bash
vol -f memory.raw windows.info
```

### What is the Linux kernel version?

```bash
vol -f memory.raw linux.banner
```

---

## 02 - Process Enumeration (Core Investigation)

### What processes were running?

```bash
vol -f memory.raw windows.pslist
```

### What is the parent-child process relationship?

```bash
vol -f memory.raw windows.pstree
```

### Are there hidden or unlinked processes?

```bash
vol -f memory.raw windows.psscan
```

### What suspicious processes are running from Temp/AppData folders?

```bash
vol -f memory.raw windows.cmdline
```

---

## 03 - Suspicious Process Investigation

### What is the command line used by a suspicious process?

```bash
vol -f memory.raw windows.cmdline --pid <PID>
```

### What DLLs are loaded by the suspicious process?

```bash
vol -f memory.raw windows.dlllist --pid <PID>
```

### What handles are opened by the suspicious process?

```bash
vol -f memory.raw windows.handles --pid <PID>
```

### What is the process tree of a suspicious PID?

```bash
vol -f memory.raw windows.pstree --pid <PID>
```

### What privileges does the suspicious process have?

```bash
vol -f memory.raw windows.privs --pid <PID>
```

----

## 04 - Network Connections (C2 Detection Layer)

### What network connections were active / Which processes are communicating externally?

```bash
vol -f memory.raw windows.netscan
```

---

## - 05 Malware Persistence Mechanisms 

### Are there malicious Run/RunOnce registry keys? 

```bash
vol -f memory.raw windows.registry.printkey
```

### Are there suspicious services installed?

```bash
vol -f memory.raw windows.services
```

### Are there malicious scheduled tasks? 

```bash
vol -f memory.raw windows.scheduledtasks
```
