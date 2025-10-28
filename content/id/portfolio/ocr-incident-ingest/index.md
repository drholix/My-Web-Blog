+++
title = "Pipeline OCR Incident"
date = 2024-04-08T14:45:00+07:00
summary = "Workflow OCR yang mengekstrak indikator dari laporan insiden PDF."
description = "Proyek triase incident berbasis OCR yang mengubah PDF menjadi IOC terstruktur menggunakan fungsi serverless dan validasi."
tags = ["Portfolio", "OCR", "Automation"]
cover = "cover.svg"
+++

Agar laporan insiden dari vendor lebih mudah ditindak, aku membuat pipeline OCR:

- AWS Textract membaca PDF dan mengekstrak IP, domain, serta hash.
- Validator Python menandai indikator yang tidak valid dan memberi skor kepercayaan.
- Hasil bersih tersinkron ke MISP dan ServiceNow sehingga analis langsung menjalankan playbook.

Pipeline ini memproses 120+ laporan per pekan dan hampir menghapus kesalahan input manual.
