+++
title = "CTF Guide: Blue Team Playbook"
date = 2024-03-04T01:00:00Z
summary = "A fast-response checklist to help SOC teams during CTF competitions."
description = "Step-by-step blue team playbook for CTF events covering log collection, triage, and response handoffs."
tags = ["CTF", "SIEM", "Threat Hunting"]
categories = ["Cybersecurity"]
cover = "cover.svg"
featured = true
authors = ["Alief Kurniawan"]
+++

Welcome to the condensed playbook I rely on when supporting the **Blue Team** during CTF events. The structure follows three phases: _collect_, _triage_, and _respond_.

1. **Collect:** verify that all critical logs (auth, DNS, proxy) reach the SIEM. Reuse saved searches for the most common IOCs.
2. **Triage:** prioritize alerts with MITRE ATT&CK context. Flag false positives so the team does not see them again.
3. **Respond:** document host isolation, credential resets, and stakeholder communication.

{{< alert type="info" title="Checklist" >}}
Review this runbook before the competition to ensure every log pipeline stays active.
{{< /alert >}}

{{< iframe src="https://www.youtube.com/embed/Bd6zyj3Tiu4" title="Playbook Demo" allowfullscreen="true" >}}

Sample Sigma query for Splunk:

```splunk
index=ctf action=blocked sourcetype=proxy earliest=-24h
| stats count by src_ip dest_domain
| sort - count
```

Example GitOps workflow for storing Splunk dashboards:

```yaml
name: sync-splunk-dashboards
on:
  push:
    paths:
      - "dashboards/**"
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Push dashboard to Splunk
        run: ./scripts/push-dashboard.sh
```
