+++
title = "Hardening Wazuh untuk SOC"
date = 2024-01-15T10:15:00+07:00
summary = "Checklist pengamanan Wazuh Server, Agent, dan dashboard agar siap audit."
description = "Checklist pengamanan Wazuh berbahasa Indonesia mencakup TLS mutual, RBAC dashboard, lifecycle log, dan backup harian."
tags = ["Wazuh", "Hardening", "Blue Team"]
categories = ["Operations"]
cover = "cover.svg"
+++

Wazuh adalah fondasi monitoring open-source favoritku. Berikut checklist hardening yang selalu kupakai:

- Aktifkan TLS mutual antara agent dan manager.
- Terapkan _role-based access control_ pada Wazuh Dashboard.
- Gunakan _index lifecycle management_ di OpenSearch agar log lama otomatis dihapus.

Contoh snippet konfigurasi untuk memaksa TLS 1.2:

```yaml
# /var/ossec/etc/ossec.conf
<remote>
  <connection>secure</connection>
  <protocol>tcp</protocol>
  <port>1514</port>
  <allowed-ips>10.0.0.0/24</allowed-ips>
</remote>
```

Langkah lanjutan termasuk _backup_ harian dan monitoring integritas file.
