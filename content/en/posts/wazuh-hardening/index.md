+++
title = "Hardening Wazuh for the SOC"
date = 2024-01-15T03:15:00Z
summary = "A security checklist for Wazuh server, agent, and dashboard readiness."
description = "Checklist for securing Wazuh deployments covering mutual TLS, RBAC, lifecycle management, and daily backup routines."
tags = ["Wazuh", "Hardening", "Blue Team"]
categories = ["Operations"]
cover = "cover.svg"
+++

Wazuh is my favorite open-source monitoring stack. These hardening steps keep it audit-ready:

- Enable mutual TLS between agents and the manager.
- Apply role-based access control in Wazuh Dashboard.
- Enable OpenSearch index lifecycle management to retire aged logs automatically.

Snippet to enforce TLS 1.2:

```yaml
# /var/ossec/etc/ossec.conf
<remote>
  <connection>secure</connection>
  <protocol>tcp</protocol>
  <port>1514</port>
  <allowed-ips>10.0.0.0/24</allowed-ips>
</remote>
```

Follow-up steps cover daily backups and file-integrity monitoring.
