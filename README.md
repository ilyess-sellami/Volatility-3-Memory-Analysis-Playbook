# Volatility 3 Memory Analysis Playbook

This playbook standardizes the analysis of memory dumps using **[Volatility 3](https://github.com/volatilityfoundation/volatility3)** to:

- Identify **malicious processes**
- Detect persistence mechanisms
- Extract network indicators (C2, sockets, connections)
- Reconstruct attacker behavior from volatile memory
- Correlate memory artifacts with incident timeline

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
