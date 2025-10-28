+++
title = "Wazuh Lab Blueprint"
date = 2024-03-14T11:30:00Z
summary = "Hands-on Wazuh lab with scripted provisioning, attack replay, and detection baselines."
description = "Portable Wazuh lab project featuring automated provisioning, replayable attack scenarios, and baseline dashboards for analyst training."
tags = ["Portfolio", "Wazuh", "Lab"]
cover = "cover.svg"
+++

This lab provides a reproducible Wazuh environment for onboarding analysts:

- Terraform scripts spin up Elastic, Wazuh server, and vulnerable hosts in under 15 minutes.
- Ansible playbooks load baseline dashboards, detection rules, and sample alerts.
- Atomic Red Team scenarios replay the attacks so trainees can validate detections.

Documentation includes a two-hour workshop guide and remediation checklist for each exercise.
