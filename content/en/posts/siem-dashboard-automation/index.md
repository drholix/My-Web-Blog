+++
title = "Automating SIEM Dashboards"
date = 2024-02-21T02:30:00Z
summary = "Packaging SIEM dashboards through GitOps for traceable audits and effortless rollback."
description = "Guide to automating SIEM dashboard deployment with GitOps pipelines, API publishing, and compliance-friendly auditing."
tags = ["SIEM", "Automation", "GitOps"]
categories = ["Engineering"]
cover = "cover.svg"
featured = true
+++

Dashboards are the single source of truth for SOC analysts. To keep changes under control I built a GitOps pipeline:

- Export vendor-native formats (Splunk SimpleXML, Kibana NDJSON, Wazuh JSON).
- Store them in Git and require code reviews.
- Deploy through API calls with service account tokens.

{{< highlight bash >}}
# example push to Wazuh
curl -X POST "https://wazuh.local:55000/splunk" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d @dashboards/sso-monitoring.json
{{< /highlight >}}

For compliance the audit logging pipeline ensures every change includes a git signature.

Here is a quick image optimization example using the HBS width query:

![Dashboard Preview](/images/dashboard-card.svg?width=960)

For heavier processing rely on the `processed-image` shortcode within the same page bundle:

{{< processed-image src="cover.svg" alt="Dashboard Screenshot" width="720" caption="Resized with Hugo Pipes" >}}
