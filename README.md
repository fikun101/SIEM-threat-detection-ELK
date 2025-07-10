# SIEM-threat-detection-ELK

## Overview
This project demonstrates how to configure the ELK Stack (Elasticsearch, Logstash, Kibana) on Kali Linux to ingest, parse, and analyze system logs for threat detection. It focuses on monitoring `/var/log/auth.log` to identify suspicious authentication activity, such as brute-force login attempts and unauthorized user creation.

## Objectives
- Install and configure ELK Stack on Kali Linux
- Ingest and parse authentication logs using Logstash
- Visualize log data in Kibana
- Detect security events such as failed logins and user creation

## Tools Used
- Elasticsearch 7.x
- Logstash 7.x
- Kibana 7.x
- rsyslog (to generate `/var/log/auth.log`)
- Test tools: `sudo`, `hydra`, `useradd`, `curl`

## File Structure
```
elk-log-analysis/
├── README.md
├── configs/
│   └── syslog.conf
├── dashboard/
│   └── kibana-authlog-dashboard.ndjson
├── detections/
│   └── brute-force.md
│   └── user-creation.md
├── screenshots/
│   └── kibana-dashboard.png
├── report/
│   └── ELK_Threat_Detection_Report.md
```

## Setup Instructions
1. Install OpenJDK, ELK Stack, and rsyslog
2. Enable and start Elasticsearch, Logstash, and Kibana services
3. Create a custom Logstash config at `/etc/logstash/conf.d/syslog.conf`
4. Run Logstash to ingest logs from `/var/log/auth.log`
5. Access Kibana at `http://localhost:5601` and create an index pattern

## Sample Logstash Configuration
Located in `configs/syslog.conf`:
```conf
input {
  file {
    path => "/var/log/auth.log"
    start_position => "beginning"
    sincedb_path => "/dev/null"
  }
}

filter {
  grok {
    match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{HOSTNAME:host} %{DATA:process}(?:\[%{POSINT:pid}\])?: %{GREEDYDATA:msg}" }
  }
}

output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "authlog-%{+YYYY.MM.dd}"
  }
}
```

## Dashboard
Import the file at `dashboard/kibana-authlog-dashboard.ndjson` into Kibana to view authentication-related visualizations.

## Simulated Events
- Multiple failed `sudo` attempts
- SSH brute-force via `hydra`
- New user creation via `sudo useradd attacker`

## License
This project is created for educational use in a secure virtual environment. No production systems were used or affected.
