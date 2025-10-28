+++
title = "Dashboard Intel ThreatLens"
date = 2024-05-01T16:00:00+07:00
summary = "Workspace ThreatLens kustom yang menggabungkan feed intel, cakupan Sigma, dan aksi siap pakai untuk SOC."
description = "Proyek dashboard ThreatLens yang mengonsolidasikan sumber intelijen ancaman, mapping ATT&CK, dan penugasan respons untuk SOC."
tags = ["Portfolio", "ThreatLens", "Intelligence"]
cover = "cover.svg"
+++

Aku membangun dashboard ThreatLens yang menggabungkan feed vendor dengan telemetry internal agar analis bergerak lebih cepat:

- Mengintegrasikan MISP, CISA KEV, dan hasil honeypot internal ke _queue_ tunggal.
- Menghasilkan _heatmap_ ATT&CK, skor cakupan Sigma, dan tiket remidiasi terbuka.
- Mengekspor _digest_ mingguan via Netlify Functions langsung ke Slack dan email list.

Hasilnya adalah pandangan 360° tentang siapa yang menargetkan kami, seberapa siap kontrol yang ada, dan playbook mana yang perlu diperbarui.
