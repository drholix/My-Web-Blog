+++
title = "ThreatLens Intelligence Dashboard"
date = 2024-05-01T09:00:00Z
summary = "Custom ThreatLens workspace aggregating intel feeds, Sigma coverage, and SOC-ready actions."
description = "ThreatLens dashboard project that consolidates threat intelligence sources, ATT&CK mapping, and response assignments for the SOC."
tags = ["Portfolio", "ThreatLens", "Intelligence"]
cover = "cover.svg"
+++

I built a ThreatLens dashboard that merges vendor feeds with internal telemetry so analysts can react faster:

- Integrated MISP, CISA KEV, and local honeypot results into a unified queue.
- Generated ATT&CK heatmaps, Sigma coverage scores, and open remediation tickets.
- Exported weekly digests via Netlify Functions straight into Slack and email lists.

The result is a 360° view of who is targeting us, how prepared we are, and which playbooks must be updated next.
