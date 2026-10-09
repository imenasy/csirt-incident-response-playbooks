markdown
# Playbook 03: Distributed Denial of Service (DDoS) on Digital Banking Rails

## 1. Trigger Conditions
- Internet edge bandwidth utilization > 85% with dropping legitimate user sessions.
- Inbound SYN flood, DNS amplification, or Layer 7 HTTPS flood targeting USSD/Mobile Banking endpoints.

## 2. Mitigation Procedure
1. Confirm attack type (Layer 3/4 volumetric vs. Layer 7 application resource exhaustion).
2. Activate ISP BGP Flowspec with national telecommunication up-link providers (MTN/Airtel/Liquid Telecom) to scrub traffic upstream.
3. Enable Cloud/Edge WAF **"Under Attack Mode"** (strict challenge-response, JavaScript puzzles).
4. Restrict RIPPS/RNDPS settlement gateway ingress to whitelisted central clearing IP prefixes only.
5. Continuously report API availability metrics to Head of IT and executive steering committee.
