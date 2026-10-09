# Playbook 01: Core Banking Infrastructure Ransomware Outbreak

## Phase 1: Immediate Triage & Severity Confirmation (Minute 0 – 15)
1. Verify alert triggered by CrowdStrike Falcon XDR or SOC SIEM indicating suspicious file encryption, volume shadow copy deletion, or known malware hash execution.
2. Declare **P1 Major Cyber Incident**. Notify Senior Manager – Cybersecurity and Head of IT.

## Phase 2: Containment & Network Isolation (Minute 15 – 30)
1. **Network Containment:** Issue immediate host containment command via CrowdStrike console for infected nodes.
2. **Perimeter Action:** Execute emergency network script to isolate the impacted District SACCO branch VLAN:
   ```bash
   ssh admin@core-fw.sacco.rw "config firewall policy ; edit 101 ; set status disable ; end"
Sever inter-branch VPN between infected branch and central Core Banking cluster.

Preserve Volatile Memory: Before powering down any host, execute live RAM acquisition on the hypervisor level (FTK Imager CLI or ESXi memory dump).

Phase 3: Eradication & Recovery (Hour 1 – 6)
Re-image infected hosts using verified golden images from hardened templates.

Validate integrity of immutable offline/WORM backups.

Coordinate with Senior Manager – Infrastructure & Operations for database Point-In-Time Recovery (PITR) to pre-infection timestamp.

Restore connectivity under deep-packet inspection monitoring.

Phase 4: Root Cause Analysis (RCA) & Regulatory Disclosure
Complete forensic artifact timeline (entry vector, patient zero, lateral traversal).

Prepare BNR Regulatory Incident Brief within 24 hours.


