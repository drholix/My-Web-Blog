+++
title = "Blueprint Briefing Intel Mingguan"
date = 2024-04-18T12:55:00+07:00
summary = "Alur berulang untuk mengubah feed intel jadi briefing SOC yang actionable setiap Senin."
description = "Blueprint briefing intel mingguan berbahasa Indonesia yang mencakup koleksi, prioritas, dan tindakan pemangku kepentingan."
tags = ["Threat Intelligence", "Briefing", "SOC"]
categories = ["Operations"]
cover = "cover.svg"
authors = ["Alief Kurniawan"]
+++

Setiap Senin aku menyampaikan briefing intel 15 menit ke SOC. Format ini menjaga sinyal tetap tinggi:

1. **Koleksi:** kurasi dari MISP, ThreatFox, dan advisori pemerintah. Tag tiap item dengan relevansi industri.
2. **Prioritas:** beri skor berdasarkan exploitability, target aktif, dan ketersediaan deteksi.
3. **Aksi:** cantumkan runbook, update deteksi, dan pemilik tiket.

```json
{
  "tanggal_briefing": "2024-04-15",
  "prioritas": "tinggi",
  "kampanye": "Storm-1814",
  "aksi_diperlukan": [
    "Deploy Sigma rule baru",
    "Perbarui kebijakan O365 safe links"
  ]
}
```

{{< alert type="primary" title="Distribusi" >}}
Kirim slide, ringkasan JSON, dan diff Sigma dalam satu paket agar engineering dan manajemen melihat konteks yang sama.
{{< /alert >}}
