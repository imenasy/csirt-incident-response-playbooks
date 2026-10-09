Markdown
# Playbook 01: Core Banking Infrastructure Ransomware Outbreak

## 1. Overview & Classification
- **Classification:** P1 – Critical Emergency (Immediate business impact).
- **Scope:** Hypervisors, database hosts, application middleware, and branch local networks across 30 District SACCOs.
- **Authority:** Initiated by SOC Lead Analyst; managed by Senior Manager – Cybersecurity, Risk & Compliance as Incident Commander.

---

## 2. Phase 1: Identification & Initial Scoping (0 – 15 Minutes)
1. **Trigger Alert:** Telemetry from CrowdStrike Falcon, Windows Event ID 4663 (abnormal mass file access), or bulk file modification alerts on NFS storage.
2. **Host Triaging:** Confirm encryption extension pattern (e.g., `.locked`, `.enc`), execution of volume shadow deletion commands (`vssadmin delete shadows /all /quiet`), or presence of ransom drop-files.
3. **Escalation:** SOC Analyst initiates automated dial-out to Incident Commander and Head of IT.

---

## 3. Phase 2: Immediate Containment & Network Micro-Isolation (15 – 30 Minutes)

### Action A: Endpoint & Network Quarantine
Isolate the infected subnets immediately to prevent lateral traversal (SMB/RPC port 445/135) to Core Banking and Payment Gateways:

```bash


# FortiGate / Core Firewall Emergency VLAN Isolation CLI
config firewall policy
    edit 201
        set name "EMERGENCY_ISOLATE_DSACCO_BRANCH_07"
        set srcintf "VLAN_BRANCH_07"
        set dstintf "CBS_CORE_ZONE"
        set status disable
    next
end
Action B: CrowdStrike Falcon API Network Containment
Bash
# Force host network isolation via Falcon API
curl -X POST "[https://api.crowdstrike.com/devices/entities/devices-actions/v1?action_name=contain](https://api.crowdstrike.com/devices/entities/devices-actions/v1?action_name=contain)" \
  -H "Authorization: Bearer ${FALCON_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{"ids": ["a89012bc34de56fa"]}'
Action C: Memory Preservation Before Power Action
Do not reboot or power cycle running machines. Capture volatile RAM for key-extraction:

```

# Hypervisor-level memory snapshot via ESXi Shell
vim-cmd vmsvc/snapshot.create <VM_ID> "IR_RAM_DUMP" "Forensic Memory Preservation" 1 0

## 4. Phase 3: Eradication & System Recovery (Hours 1 – 6)
**Malware Vector Identification:** Locate initial vector (e.g., unpatched edge VPN appliance, credential compromise, spear-phishing).

**Directory Services Audit:** Rotate all Domain Controller Krbtgt account passwords twice; invalidate Kerberos ticket grants.

**WORM Backup Verification:** Verify integrity of air-gapped, immutable Veeam/ZFS storage snapshots prior to restore operations.

**Restoration Priority:**

**Step 1:** Active Directory & PKI root services.

**Step 2:** Core Banking PostgreSQL/Oracle settlement databases.

**Step 3:** RIPPS  / RNDPS payment interconnect nodes.

**Step 4:** District SACCO branch reporting servers.

## 5. Phase 4: Regulatory Disclosures & Post-Mortem
**BNR Compliance Notification:** Submit the initial BNR Cyber Incident Notification within the statutory 2-hour window.

**Data Protection Authority Notice:** Complete Law Nº 058/2021 Data Protection breach advisory within 48 hours to the National Cyber Security Authority (NCSA).

**Post-Incident Review (PIR):** Convene blameless retrospective with Head of IT and Senior Managers within 5 business days. Document root-cause timeline and lessons learned.
