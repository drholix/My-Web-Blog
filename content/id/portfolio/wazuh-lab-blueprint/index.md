+++
title = "Blueprint Lab Wazuh"
date = 2024-03-14T18:30:00+07:00
summary = "Lab Wazuh siap praktik dengan provisioning terotomasi, replay serangan, dan baseline deteksi."
description = "Proyek lab Wazuh portabel yang berisi provisioning otomatis, skenario serangan ulang, dan dashboard baseline untuk pelatihan analis."
tags = ["Portfolio", "Wazuh", "Lab"]
cover = "cover.svg"
+++

Lab ini menyediakan lingkungan Wazuh yang dapat direplikasi untuk onboarding analis:

- Skrip Terraform menyiapkan Elastic, server Wazuh, dan host rentan dalam 15 menit.
- Playbook Ansible memuat dashboard baseline, aturan deteksi, dan contoh alert.
- Skenario Atomic Red Team memutar ulang serangan agar peserta bisa menguji deteksi.

Dokumentasi mencakup panduan workshop dua jam dan checklist remidiasi untuk tiap latihan.
