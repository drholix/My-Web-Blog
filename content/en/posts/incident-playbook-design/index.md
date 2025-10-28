+++
title = "Designing Incident Playbooks that Scale"
date = 2024-04-02T05:20:00Z
summary = "A modular approach to incident playbooks that adapts to new detections without rewriting everything."
description = "How to design scalable incident response playbooks with modular phases, approval matrices, and reusable automation hooks."
tags = ["Incident Response", "Playbook", "Automation"]
categories = ["Process"]
cover = "cover.svg"
authors = ["Alief Kurniawan"]
+++

When a new detection fires, the playbook should be ready without weeks of drafting. I break every runbook into reusable blocks:

- **Trigger:** detection source, severity, and mapping to MITRE ATT&CK.
- **Scope:** assets, identities, and regulatory impact.
- **Actions:** human tasks vs automation plus the RACI table.

```yaml
playbook:
  id: phishing-lateral
  version: 2024.2
  trigger:
    detection: microsoft-identity-risk
    severity: high
  actions:
    - name: disable-compromised-user
      owner: identity
      automation: azure_ad_disable_user
    - name: sweep-mailboxes
      owner: soc
      automation: o365_purge_campaign
```

Every block lives in its own file so new detections simply import the relevant steps. The result: less drift, faster onboarding, and measurable MTTR improvements.
