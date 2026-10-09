# Playbook 01: Core Banking Infrastructure Ransomware Outbreak

## Phase 1: Immediate Triage & Severity Confirmation (Minute 0 – 15)
1. Verify alert triggered by CrowdStrike Falcon XDR or SOC SIEM indicating suspicious file encryption, volume shadow copy deletion, or known malware hash execution.
2. Declare **P1 Major Cyber Incident**. Notify Senior Manager – Cybersecurity and Head of IT.

## Phase 2: Containment & Network Isolation (Minute 15 – 30)
1. **Network Containment:** Issue immediate host containment command via CrowdStrike console for infected nodes.
2. **Perimeter Action:** Execute emergency network script to isolate the impacted District SACCO branch VLAN:
   ```bash
   ssh admin@core-fw.sacco.rw "config firewall policy ; edit 101 ; set status disable ; end"
