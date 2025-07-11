# ELK Threat Detection Project Report

## Project Title
Log Analysis and Threat Detection Using ELK Stack on Kali Linux

## Objective
To set up a Security Information and Event Management (SIEM) solution using the ELK Stack, ingest and parse system logs, and detect threat indicators such as brute-force login attempts and unauthorized user creation.

## Tools and Environment
- **Operating System:** Kali Linux
- **SIEM Stack:** Elasticsearch, Logstash, Kibana (7.x)
- **Log Source:** `/var/log/auth.log`
- **Simulated Attacks:** SSH brute-force, unauthorized user creation
- **Test Tools:** Hydra, sudo, useradd

## Log Pipeline Overview
- **Logstash Config:** `configs/syslog.conf`
- **Input:** Reads `/var/log/auth.log`
- **Filter:** Parses logs using Grok patterns
- **Output:** Sends parsed data to Elasticsearch under `authlog-*` index

## Simulated Threats and Detections

### 1. SSH Brute Force
- Simulated with `hydra` targeting local SSH
- Multiple `Failed password` entries generated
- Detected using Kibana filters and visualizations
- See: `detections/brute-force.md`

### 2. Unauthorized User Creation
- Simulated with `sudo useradd attacker_test`
- Detected entries like `useradd: new user added 'attacker_test'`
- Tracked using Discover and dashboard visualizations
- See: `detections/user-creation.md`

## Kibana Dashboard
- Visualizations created and saved to dashboard:
  - Failed SSH login bar chart
  - User creation event table
- Dashboard exported as `dashboard/kibana-authlog-dashboard.ndjson`

## Outcome
- Logs successfully ingested and parsed
- Threat activity clearly visualized in Kibana
- Demonstrates capability to use ELK as a basic SIEM for Linux environments

## Ethical Disclaimer
This project was conducted in a controlled, isolated environment on Kali Linux VMs. No real networks, production systems, or external data sources were used. All attacks were simulated for academic and portfolio purposes only.
