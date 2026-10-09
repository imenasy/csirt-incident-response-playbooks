markdown
# Computer Security Incident Response Team (CSIRT) Playbooks

Production-grade emergency playbooks aligned with NIST SP 800-61 r2 and ISO/IEC 27035, specifically written for tier-one financial institutions and payment gateways.

## Response Matrix
- **PB-01:** Ransomware detection, containment, network micro-isolation, and recovery without data loss.
- **PB-02:** Switch fraudulent clearing / unauthorized fund transfer containment and BNR notification protocol.
- **PB-03:** DDoS mitigation against public SACCO web portals and digital mobile banking APIs.



*playbooks/pb02_unauthorized_fund_transfer.md*:

markdown
# Playbook 02: Switch Fraud & Unauthorized Mass Fund Transfers

### 1. Phase 1: Identification & Immediate Verification (0 - 15 Mins)
- Verify alert triggering from SIEM: velocity surge > 500% normal threshold or anomalous origin IP.
- Confirm transaction clearing status with RIPPS/RNDPS settlement operator.

### 2. Phase 2: Containment (15 - 30 Mins)
- Execute emergency API revocation on the switch gateway:
  `./scripts/revoke_switch_token.sh --partner-id=SUSPICIOUS_ID`
- Place immediate hold on receiving internal accounts via CBS core API.
- Isolate the originating application server using CrowdStrike network containment.

### 3. Phase 3: Regulatory & Executive Notification
- Brief Head of IT within 30 minutes of confirmed incident.
- Initiate BNR Major Incident Report within statutory hours per BNR Cybersecurity Regulations.



---
