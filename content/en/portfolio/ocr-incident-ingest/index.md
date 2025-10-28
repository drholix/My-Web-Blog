+++
title = "OCR Triage Pipeline"
date = 2024-04-08T07:45:00Z
summary = "Optical character recognition workflow that extracts indicators from PDF incident reports."
description = "OCR incident triage project turning PDF submissions into structured IOCs using serverless functions and validation."
tags = ["Portfolio", "OCR", "Automation"]
cover = "cover.svg"
+++

To keep vendor incident reports actionable I created an OCR pipeline:

- AWS Textract parses PDF submissions and extracts IPs, domains, and hashes.
- Python validators flag malformed indicators and tag them with confidence scores.
- Clean results sync to MISP and ServiceNow so analysts can launch playbooks instantly.

The pipeline processes 120+ reports per week and reduces manual typing errors to nearly zero.
