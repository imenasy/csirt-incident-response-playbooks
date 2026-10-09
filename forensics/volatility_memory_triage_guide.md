# Volatility 3 Memory Forensic Acquisition & Analysis SOP

## 1. Triage Commands for Compromised Banking Hosts
When memory image (`memdump.raw`) is collected from an infected core system host:

```bash
# 1. Identify active processes and hidden injection threads
python3 vol.py -f memdump.raw windows.pslist
python3 vol.py -f memdump.raw windows.malfind

# 2. Check established network sockets at time of compromise
python3 vol.py -f memdump.raw windows.netscan | grep -E "ESTABLISHED|SYN_SENT"

# 3. Detect injected DLLs or unauthorized API hooking
python3 vol.py -f memdump.raw windows.dlllist

# 4. Dump suspicious process memory for static malware extraction
python3 vol.py -f memdump.raw -o ./dumps windows.dumpfiles --pid <SUSPICIOUS_PID>
