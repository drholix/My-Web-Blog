+++
title = "Panduan CTF: Blue Team Playbook"
date = 2024-03-04T08:00:00+07:00
summary = "Kerangka investigasi cepat untuk tim SOC saat menghadapi serangan berbasis CTF."
description = "Playbook Blue Team berbahasa Indonesia untuk lomba CTF dengan langkah pengumpulan log, triase, dan respons."
tags = ["CTF", "SIEM", "Threat Hunting"]
categories = ["Cybersecurity"]
cover = "cover.svg"
featured = true
authors = ["Alief Kurniawan"]
+++

Selamat datang di ringkasan playbook yang biasa kupakai ketika membantu tim **Blue Team** saat ajang CTF. Struktur dasarnya terdiri dari tiga fase: _collect_, _triage_, dan _respond_.

1. **Collect:** pastikan semua log kritikal (auth, DNS, proxy) sudah masuk SIEM. Gunakan fitur _saved search_ untuk IOC yang paling umum.
2. **Triage:** prioritaskan alert dengan konteks MITRE ATT&CK. Tandai _false positive_ agar tak muncul lagi.
3. **Respond:** dokumentasikan langkah isolasi host, reset kredensial, serta komunikasi ke stakeholder.

{{< alert type="info" title="Checklist" >}}
Gunakan _runbook_ ini sebelum kompetisi untuk memastikan semua pipeline log aktif.
{{< /alert >}}

{{< iframe src="https://www.youtube.com/embed/Bd6zyj3Tiu4" title="Demo Playbook" allowfullscreen="true" >}}

Contoh _query_ Sigma ke Splunk:

```splunk
index=ctf action=blocked sourcetype=proxy earliest=-24h
| stats count by src_ip dest_domain
| sort - count
```

Dan contoh _workflow_ GitOps yang kubuat untuk menyimpan _dashboard_ Splunk:

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
