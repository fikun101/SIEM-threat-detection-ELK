# Detection: Unauthorized User Account Creation

## Description
Identifies unauthorized or suspicious user account creation on a Linux system by monitoring system authentication logs.

## Log Source
`/var/log/auth.log`

## Log Event Triggered By
Simulating user creation via:
```bash
sudo useradd attacker_test
```

## How to Detect in Kibana
1. Open Kibana at `http://localhost:5601`
2. Go to **Discover** and use index pattern: `authlog-*`
3. Search the following filter:
```
message: "useradd"
```
4. Visualize with a table or bar chart showing user creation over time or by host

## Result
- Matching entries such as:
  `useradd[12345]: new user added 'attacker_test'`
- Events appear in Discover and can be visualized in the dashboard

## Notes
Frequent or unexpected user account creation should be flagged, especially outside normal admin operations. This is often an early indicator of privilege escalation or attacker persistence.
