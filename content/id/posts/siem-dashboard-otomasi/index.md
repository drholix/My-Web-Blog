+++
title = "Membangun Otomasi Dashboard SIEM"
date = 2024-02-21T09:30:00+07:00
summary = "Cara mengemas dashboard SIEM ke GitOps sehingga audit dan rollback menjadi mudah."
description = "Panduan otomasi dashboard SIEM dalam Bahasa Indonesia lengkap dengan pipeline GitOps, API deployment, dan audit compliance."
tags = ["SIEM", "Automation", "GitOps"]
categories = ["Engineering"]
cover = "cover.svg"
featured = true
+++

Dashboards kerap menjadi _single source of truth_ bagi analis SOC. Agar perubahan tetap terkontrol, aku membangun pipeline GitOps:

- Gunakan format JSON/YAML resmi vendor (Splunk SimpleXML, Kibana NDJSON, Wazuh JSON).
- Simpan dalam repo Git dan aktifkan _code review_.
- Deploy via API menggunakan token service account.

{{< highlight bash >}}
# contoh deploy ke Wazuh
curl -X POST "https://wazuh.local:55000/splunk" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d @dashboards/sso-monitoring.json
{{< /highlight >}}

Untuk _compliance_, audit log pipeline memastikan setiap perubahan memiliki _signature_ git.

Berikut contoh optimasi gambar versi cepat menggunakan query milik tema HBS:

![Preview Dashboard](/images/dashboard-card.svg?width=960)

Jika ingin pemrosesan lebih lanjut, gunakan shortcode `processed-image` pada _page bundle_ yang sama:

{{< processed-image src="cover.svg" alt="Screenshot Dashboard" width="720" caption="Output setelah resize Hugo Pipes" >}}
