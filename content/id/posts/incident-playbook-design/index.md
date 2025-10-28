+++
title = "Merancang Playbook Insiden yang Skalabel"
date = 2024-04-02T12:20:00+07:00
summary = "Pendekatan modular agar playbook insiden siap menghadapi deteksi baru tanpa ditulis ulang."
description = "Cara merancang playbook incident response yang skalabel dengan fase modular, matriks persetujuan, dan kait otomasi reusable."
tags = ["Incident Response", "Playbook", "Automation"]
categories = ["Process"]
cover = "cover.svg"
authors = ["Alief Kurniawan"]
+++

Saat deteksi baru muncul, playbook harus langsung siap tanpa penulisan berhari-hari. Aku membaginya ke blok yang bisa dipakai ulang:

- **Trigger:** sumber deteksi, tingkat keparahan, dan mapping MITRE ATT&CK.
- **Scope:** aset, identitas, dan dampak regulasi.
- **Actions:** tugas manusia vs otomasi lengkap dengan tabel RACI.

```yaml
playbook:
  id: phishing-lateral
  version: 2024.2
  trigger:
    detection: microsoft-identity-risk
    severity: high
  actions:
    - name: nonaktifkan-akun
      owner: identity
      automation: azure_ad_disable_user
    - name: bersihkan-mailbox
      owner: soc
      automation: o365_purge_campaign
```

Setiap blok kusimpan di berkas terpisah sehingga deteksi baru tinggal mengimpor langkah yang relevan. Dampaknya: lebih sedikit _drift_, onboarding cepat, dan MTTR yang terukur.
