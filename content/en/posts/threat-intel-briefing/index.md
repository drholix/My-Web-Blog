+++
title = "Weekly Threat Intelligence Briefing Blueprint"
date = 2024-04-18T05:55:00Z
summary = "A repeatable flow to turn intel feeds into actionable SOC briefings every Monday."
description = "Blueprint for weekly threat intelligence briefings covering collection, prioritisation, and stakeholder actions."
tags = ["Threat Intelligence", "Briefing", "SOC"]
categories = ["Operations"]
cover = "cover.svg"
authors = ["Alief Kurniawan"]
+++

Every Monday I deliver a 15-minute intel briefing to the SOC. The format keeps signal high and noise low:

1. **Collection:** curate from MISP, ThreatFox, and government advisories. Tag each item with industry relevance.
2. **Prioritisation:** score entries via exploitability, active targeting, and available detections.
3. **Action:** list runbooks, detection updates, and ticket owners.

```json
{
  "briefing_date": "2024-04-15",
  "priority": "high",
  "campaign": "Storm-1814",
  "required_actions": [
    "Deploy new Sigma rules",
    "Update O365 safe links policy"
  ]
}
```

{{< alert type="primary" title="Distribution" >}}
Send the slides, JSON summary, and Sigma diffs in one bundle so engineering and leadership share the same picture.
{{< /alert >}}
